# Power BI Analytics

An interactive Power BI solution was developed to support operational monitoring, sanitary analysis, financial assessment, and data quality auditing across the swine slaughter inspection process.

The reporting layer consumes the centralized tabular semantic model and provides a structured **top-down analytical experience**, allowing users to move from national and regional overviews to detailed analysis by slaughterhouse, animal holding, and condemnation reason.

## Report Structure

The report is organized into five thematic pages:

- **Slaughterhouses:** slaughter volumes, condemnation rates, regional distribution, operational benchmarking, and identification of high-risk establishments.
- **Animal Holdings:** production characteristics, sanitary performance, origin analysis, and comparison of local and regional slaughter flows.
- **Condemnation Reasons:** detailed analysis of sanitary causes, syndromes, temporal patterns, incidence rates, and financial impact.
- **Financial Performance:** potential and realized value, estimated losses, financial efficiency, pork price trends, and market volatility.
- **Data Quality & Audit:** traceability gaps, missing origin records, unavailable market prices, and regional data completeness.

Global date, region, and production-system filters preserve the analytical context across the report pages.

## Analytical Features

The report includes:

- Interactive KPIs and performance indicators.
- Drill-down and drill-up through temporal, geographic, and sanitary hierarchies.
- Dynamic metric selection using Calculation Groups.
- Time Intelligence analysis, including MoM, YoY, YTD, and Moving Annual Total.
- Conditional formatting to identify critical sanitary performance.
- Scatter plots for risk and outlier identification.
- Financial impact analysis by slaughterhouse and condemnation reason.
- Synchronized slicers and cross-page filtering.

## Executive Dashboard

A single-page executive dashboard was created to provide a high-level snapshot of the most relevant operational, sanitary, financial, and data quality indicators.

The dashboard is designed as an entry point to the detailed report, allowing decision-makers to identify relevant issues before navigating to the corresponding analytical page.

## Data Storytelling

Bookmarks were implemented to provide guided analytical scenarios and highlight relevant patterns, including:

- Regions with contrasting slaughter volumes and condemnation rates.
- Periods with higher sanitary risk.
- Main causes of condemnation.
- Market price shocks and financial impact.
- Missing origin and market price records.

Only selected, anonymized examples are documented in this repository.

## Mobile Experience

A dedicated mobile layout was developed for all report pages.

The mobile design prioritizes:

- Persistent date context.
- Synchronized regional filters.
- Page-specific KPI cards.
- Reduced visual density.
- Native and readable navigation on smaller screens.

## Power BI App

The report and executive dashboard were published through a Power BI App, separating the private development workspace from the controlled distribution layer.

This approach allows report changes to be validated before being released to end users.

> [!NOTE]
> The original Power BI report and application are not publicly available because they are connected to confidential operational and traceability data. This folder contains selected anonymized screenshots and documentation of the analytical design.
