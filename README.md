# End-to-End Meat Inspection Analytics Platform
> An end-to-end Data Science and Business Analytics solution for swine slaughter inspection, sanitary condemnation analysis, and risk-based decision support.

## Project Overview
Food safety, animal health, and public health are deeply interconnected. Within this ecosystem, slaughterhouses represent a critical control point between primary animal production and the final consumer, where sanitary inspections play a key role in identifying potential health risks and preventing unsafe meat from entering the food chain.

In Portugal, official veterinary services collect large volumes of operational, sanitary, traceability, production, and economic data related to swine slaughter activity. However, transforming this fragmented and heterogeneous information into actionable insights remains a major analytical challenge.

This project was developed as an end-to-end Data Science and Business Analytics solution focused on swine slaughter inspection in mainland Portugal between 2011 and 2024. The main objective was to design a modern analytical platform capable of integrating multiple data sources and providing a 360-degree view of slaughter activity, sanitary condemnations, operational logistics, animal traceability, and market dynamics.

The solution simulates a data consulting project for the Portuguese Directorate-General for Food and Veterinary Affairs (DGAV), addressing a key strategic question:

> **Can the data currently collected throughout the slaughter inspection process be transformed into a reliable analytical and predictive tool to support sanitary surveillance and data-driven decision-making?**

To address this challenge, the project covers the complete data lifecycle, from raw data ingestion and transformation using a **Medallion Architecture in Microsoft Fabric** to dimensional modelling, Business Intelligence, data quality analysis, and Machine Learning.

The ultimate goal is to explore how data can support the transition from a reactive inspection model towards a more proactive and risk-based approach, contributing to food safety monitoring, epidemiological surveillance, traceability assessment, and more efficient allocation of veterinary inspection resources.

## Project Scope & Objectives
The project focuses on five main analytical and technical objectives:

- **Slaughter Activity & Logistics:** Analyze slaughter volumes, regional and temporal patterns, and operational flows across mainland Portugal.
- **Sanitary Condemnation Analysis:** Evaluate condemnation rates, identify the main causes of carcass rejection, and assess their epidemiological value.
- **Data Quality & Traceability:** Identify inconsistencies, traceability gaps, and data reliability issues across operational information systems.
- **Economic Impact Analysis:** Explore the relationship between slaughter activity, sanitary indicators, and pork market prices, while estimating the financial impact of condemned carcasses.
- **Predictive Risk Analysis:** Develop Machine Learning models to assess the feasibility of predicting condemnation rates and identify factors associated with higher sanitary risk.

Ultimately, the project aims to explore how data-driven analytics can support a more proactive and risk-based sanitary inspection model.

## Data Sources & Integration

The project integrates multiple heterogeneous datasets from official Portuguese animal health, food safety, agricultural, and market information systems.

The source data covers different stages of the swine production and slaughter lifecycle, combining operational, sanitary, geographical, traceability, production, and economic information.

### Main Data Sources

| Data Domain | Source | Main Information |
|---|---|---|
| Animal Holdings | SISS | Holding characteristics, production type, farming system, geographic coordinates, and official holding identifiers |
| Slaughter Activity | Trichinella Inspection Records | Number of slaughtered pigs, slaughterhouse, slaughter date, and holding of origin |
| Sanitary Condemnations | SIPACE Inspection Records | Post-mortem condemnation events and reasons for carcass rejection |
| Production Characteristics | DES | Herd size, animal categories, production cycle, farming system, and standardized livestock indicators |
| Slaughterhouse Operations | IS Ungulates Indicators | Slaughterhouse activity, weekly slaughter volumes, location, and operational specialization |
| Pork Market Prices | GPP Agricultural Market Information System | Weekly regional pork carcass prices between 2011 and 2024 |
| Reference & Mapping Tables | DGAV Auxiliary Tables | Standardization of condemnation reasons and mapping of animal holding identifiers |

### Data Integration Context

The datasets were originally produced by different operational systems and administrative services, resulting in significant differences in structure, granularity, nomenclature, and identifier standards.

For example, slaughter activity is available at event and slaughterhouse level, production information is periodically declared by animal holdings, and market price data is reported weekly and regionally.

The integration process therefore required the alignment of different temporal, geographic, and operational contexts within a common analytical model.

Several integration challenges were identified:

- Different temporal granularities across source systems.
- Inconsistent animal holding identifiers between operational systems.
- Free-text fields used in legacy inspection records.
- Changes in condemnation reason nomenclature between SIPACE and +SIPACE.
- Geographic alignment between animal holdings and slaughterhouses.
- Integration of sanitary, productive, operational, and economic information.

### Source Data Centralization

All source files were initially centralized in a dedicated Microsoft Fabric Lakehouse:

`lh_dsp10_source`

This Lakehouse acts as the raw source repository for the project, preserving the original files before ingestion and transformation.

The centralized source layer feeds a second Lakehouse dedicated to the Medallion Architecture, where data is progressively processed through the Bronze, Silver, and Gold layers.

The integration process ultimately enables the connection of the main stages of the analytical lifecycle:

> **Animal Origin → Production Characteristics → Slaughter Activity → Sanitary Inspection → Condemnation Outcome → Economic Context**

## Solution Architecture

The solution was implemented in **Microsoft Fabric** and designed to cover the complete data lifecycle, from raw data ingestion to Business Intelligence and predictive analytics.

The architecture combines a centralized source Lakehouse, automated notebook pipelines, a Bronze-Silver-Gold Medallion Architecture, dimensional modelling, Power BI, and Machine Learning.

The overall architecture was designed to simulate a modern enterprise data environment and demonstrate the integration of Data Engineering, Analytics Engineering, Business Intelligence, and Data Science within a single platform.

```text
┌───────────────────────────────────────────────┐
│                 DATA SOURCES                  │
│                                               │
│ SISS │ Trichinella │ SIPACE │ DES │ IS │ GPP │
└────────────────────────┬──────────────────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   Source Lakehouse  │
              │  lh_dsp10_source    │
              │      Raw Files      │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │      Pipelines      │
              │ Automated Notebooks │
              └──────────┬──────────┘
                         │
                         ▼
        ┌────────────────────────────────┐
        │      MEDALLION ARCHITECTURE    │
        │                                │
        │  BRONZE → SILVER → GOLD        │
        └───────────────┬────────────────┘
                        │
              ┌─────────┴─────────┐
              ▼                   ▼
     ┌─────────────────┐   ┌─────────────────┐
     │ Dimensional &   │   │ Machine Learning│
     │ Semantic Model  │   │    Pipeline     │
     └────────┬────────┘   └─────────────────┘
              │
              ▼
     ┌─────────────────┐
     │    Power BI     │
     │   Dashboards    │
     └─────────────────┘
```

    
## Data Architecture

The data platform follows a **Medallion Architecture**, organizing the data transformation lifecycle into Bronze, Silver, and Gold layers.

This layered approach enables the separation of raw data ingestion, data cleaning and standardization, and business-oriented analytical transformations.

### Bronze Layer — Raw Data Ingestion

The Bronze layer represents the first stage of the data pipeline and preserves the source data with minimal transformation.

Data from the source Lakehouse is ingested into Delta tables while maintaining the original structure and granularity of each dataset.

The main objectives of this layer are:

- Preserve source data for traceability and auditability.
- Convert heterogeneous source files into a standardized Delta table format.
- Maintain the original data structure before business transformations.
- Provide a reliable foundation for subsequent data processing.

### Silver Layer — Data Cleaning and Standardization

The Silver layer focuses on improving data quality, consistency, and interoperability across the different information systems.

At this stage, data cleaning and transformation rules are applied to prepare the datasets for analytical use.

Key transformations include:

- Data type validation and standardization.
- Missing value analysis and treatment.
- Duplicate detection.
- Standardization of animal holding identifiers.
- Harmonization of condemnation reason nomenclature between legacy and current systems.
- Mapping approximately 190 original condemnation descriptions into 22 standardized sanitary categories.
- Geographic and operational data enrichment.
- Identification of potential animal traceability inconsistencies.
- Data quality validation across multiple sources.

This layer plays a critical role in ensuring that data from heterogeneous operational systems can be reliably integrated and analyzed.

> **Data Engineering Challenge:**
> One of the main data quality challenges involved harmonizing approximately 190 heterogeneous condemnation descriptions from legacy inspection systems into 22 standardized sanitary categories, while also addressing inconsistencies in animal holding identifiers and traceability records.

### Gold Layer — Business-Ready Analytical Data
The Gold layer supports the main analytical domains of the project:

- Slaughter activity and temporal trends.
- Regional distribution and transportation logistics.
- Sanitary condemnation rates and rejection causes.
- Animal holding and production characteristics.
- Slaughterhouse operational profiles.
- Pork market price dynamics and economic impact analysis.
- Curated feature datasets for Machine Learning.

These datasets provide the analytical foundation for the Power BI semantic model and the predictive analysis pipeline.

## Dimensional Model & Star Schema
To support consistent, scalable, and business-oriented analytics, the project adopts a **Kimball dimensional modelling approach**.

The analytical model was structured around fact tables, which store quantitative business metrics, and dimension tables, which provide the descriptive context required for filtering, segmentation, and multidimensional analysis.

### Business Process & Bus matrix

A **Bus Matrix** was used during the modelling process to identify the main business processes and define the conformed dimensions shared across the analytical model.

The dimensional design focuses on two main business processes:

- **Sanitary Inspection Controls**, supporting the analysis of slaughter activity, tested animals, condemned animals, and condemnation rates.
- **Condemnation Events**, providing a more detailed view of the specific reasons associated with carcass rejection for human consumption.

These business processes are represented by two main fact tables:

- `Fact_controlo_sanitario`
- `Fact_reprovacoes`
  
### Fact Tables

#### Fact_controlo_sanitario

This fact table represents sanitary inspection control activity and contains the main quantitative indicators related to slaughter and condemnation events.

Key analytical measures include:

- Number of animals tested.
- Number of condemned animals.
- Sanitary condemnation rate.
- Estimated economic value of slaughtered carcasses.
- Estimated economic impact associated with condemned carcasses.

The table is linked to temporal, animal holding, slaughterhouse, and geographic dimensions.

Regional pork market prices were also incorporated into the analytical process to support the estimation of the economic value associated with slaughter and sanitary condemnation outcomes.

#### Fact_reprovacoes

This fact table provides a more granular analysis of sanitary condemnation events and their associated rejection reasons.

Each condemnation event can be analyzed according to:

- Date.
- Animal holding of origin.
- Slaughterhouse.
- Condemnation reason.
- Standardized sanitary category.
- Geographic and administrative context.

This structure supports the identification of temporal, regional, and operational patterns associated with carcass rejection.

### Dimension Tables

The dimensional model includes the following main dimensions:

| Dimension | Analytical Purpose |
|---|---|
| `Dim_date` | Supports analysis by day, week, month, quarter, and year |
| `Dim_exploracao_scd` | Describes animal holdings and preserves historical changes in production characteristics |
| `Dim_matadouro` | Contains slaughterhouse identification and operational information |
| `Dim_motivorejeicao` | Structures original condemnation reasons and standardized sanitary categories |
| `Dim_exp_geografia` | Supports geographic analysis of animal holdings |
| `Dim_mat_geografia` | Supports independent geographic analysis of slaughterhouses |

### Slowly Changing Dimension Type 2

The `Dim_exploracao_scd` dimension was modelled using a **Slowly Changing Dimension Type 2 (SCD Type 2)** approach.

This decision was required because several characteristics of an animal holding may change over time, including:

- Herd size.
- Standardized livestock units.
- Production type.
- Production cycle.
- Farming system.

Instead of overwriting historical values, the SCD Type 2 logic preserves multiple versions of the same animal holding.

A surrogate key, `SK_Marca_Historico`, is used as the technical primary key, while the original holding identifier is preserved as the natural key.

Additional temporal control fields define the validity period of each historical record:

- `data_inicio`
- `data_fim`
- `estado`

This enables each slaughter or condemnation event to be analyzed using the animal holding characteristics that were valid at the time the event occurred.

> [!NOTE]
> **Historical Traceability**
>
> The use of SCD Type 2 ensures that changes in animal holding characteristics do not overwrite historical information, preserving the correct temporal context for analytical and predictive use cases.

### Geographic Dimension Design

Two separate geographic dimensions were created for animal holdings and slaughterhouses.

Although both dimensions contain similar administrative attributes, such as regional veterinary service areas, they represent different business entities and analytical contexts.

This design enables independent analysis of:

- The geographic origin of the animals.
- The geographic location of the slaughterhouses.

Separating these dimensions also supports the analysis of transportation flows and operational relationships between production areas and slaughter locations.


