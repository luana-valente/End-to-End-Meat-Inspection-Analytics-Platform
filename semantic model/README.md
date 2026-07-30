# Semantic Model

The semantic model was developed in **Visual Studio using SQL Server Analysis Services – Tabular Mode** and deployed to Microsoft Fabric.

It provides a governed analytical layer between the Gold tables and Power BI, centralizing relationships, business logic, DAX measures, hierarchies, security, and model optimization.

## Model Design

The model follows a Star Schema and includes:

- Two fact tables for sanitary inspection controls and condemnation events.
- Dimensions for date, animal holdings, slaughterhouses, geography, and condemnation reasons.
- Many-to-one relationships between fact and dimension tables.
- Surrogate keys to support referential integrity and historical analysis.
- A calculated date table marked as the official Date Table.

## Metadata & Hierarchies

Technical fields, surrogate keys, and audit columns were hidden from report users.

Business-friendly names and analytical hierarchies were created for:

- Date.
- Administrative geography.
- DICOFRE geographic levels.
- Condemnation reasons and sanitary categories.

These hierarchies support drill-down and drill-up analysis in Power BI.

## DAX Measures & KPIs

The semantic model centralizes operational, sanitary, financial, and data quality measures.

Examples include:

- Number of slaughtered animals.
- Number of condemned animals.
- Sanitary condemnation rate.
- Estimated financial loss.
- Financial efficiency.
- Traceability and data completeness indicators.
- Condemnation incidence and financial impact by reason.

Two KPIs were created for:

- Financial efficiency.
- Sanitary condemnation rate.

## Calculation Groups

Two calculation groups were implemented:

- **Time Intelligence:** Current, MTD, QTD, YTD, PM, MoM, PY, YoY, YoY YTD, and MAT.
- **Metric Selector:** allows report users to dynamically change the metric displayed in selected visuals.

## Perspectives, Security & Partitions

The model includes:

- Financial and Data Quality perspectives.
- User roles for central administration, service administration, and external consultancy.
- Object-Level Security to restrict access to detailed animal holding information.
- Time-based partitions for large fact tables to improve processing and refresh performance.

> [!NOTE]
> The complete semantic model project is not publicly available because it contains internal connection details and project-specific metadata. This folder provides selected documentation, diagrams, and representative DAX measures.
