# IT Services Business Intelligence & AI-Assisted Analytics Dashboard

An end-to-end Power BI portfolio project for exploring the operational and financial performance of a fictional IT services business. The project combines a SQL Server data source, Power Query preparation, a Power BI data model, DAX measures, and a five-page interactive report.

> **Data notice:** This project uses synthetic data for demonstration and learning. It is not real customer, employee, financial, or operational data, and it must not be presented as proprietary data from Xscade or any other real organization.

## Project overview

The dashboard brings together client, service, project, staffing, invoice, feedback, and calendar data. It is designed to help a business user review revenue and service performance, delivery progress, client patterns, and resource utilization in one report.

### Business objectives

- Monitor invoice revenue and service performance over time.
- Review project delivery status, timelines, and workload.
- Understand client mix and engagement patterns.
- Explore employee assignments and resource utilization.
- Combine operational and financial views to support discussion and follow-up.

These are intended uses of the dashboard; validate the exact definitions and available visuals in the supplied PBIX before treating any metric as a formal business KPI.

## Tools and technologies

- Microsoft SQL Server — database and source tables
- Power Query — data import, cleanup, and transformation
- Microsoft Power BI Desktop — data modeling, DAX, and report visuals
- DAX — measures and calculated logic

## Dataset at a glance

The database is named `ITServicesBI` and contains eight tables. Counts below are the supplied project counts; row counts can differ if the local database has been changed.

| Table | Rows | Purpose |
|---|---:|---|
| `Clients` | 80 | Client entities and client attributes |
| `Services` | 8 | Service categories or offerings |
| `Projects` | 220 | Project records and delivery attributes |
| `Employees` | 45 | Employee or resource records |
| `Project_Assignments` | 709 | Employee-to-project assignment records |
| `Invoices` | 446 | Invoice or billing records |
| `Customer_Feedback` | 79 | Customer feedback records |
| `Calendar` | 2025–2026 | Date dimension covering calendar years 2025 and 2026; row count not supplied |

The project is described as using synthetic data. Confirm column names, key fields, date coverage, and row counts against the database before reproducing the model.

## Data preparation and modeling

The reported workflow is SQL Server → Power Query → Power BI model → DAX measures → report pages. Typical preparation tasks include checking data types, trimming and standardizing text, reviewing nulls and duplicates, and confirming key relationships. Document only the transformations actually present in the PBIX or Power Query steps.

Before publishing or sharing the report, verify the model's relationship keys, cardinality, filter direction, date table configuration, and whether inactive relationships are used. A likely analytical design is a calendar dimension filtering date-based facts, with client, service, project, and employee dimensions connected to relevant facts; this is a design suggestion, not a claim about the current PBIX schema.

## KPI and DAX examples

The formulas below are illustrative patterns only. They are not confirmation that measures with these names or definitions exist in the project. Replace table/column names and business rules to match the actual model. In particular, decide whether invoice revenue means invoice amount, amount paid, or another field, and whether project status values have consistent spelling.

```DAX
Total Revenue =
SUM ( Invoices[Amount] )

Invoice Count =
DISTINCTCOUNT ( Invoices[InvoiceID] )

Average Invoice Value =
DIVIDE ( [Total Revenue], [Invoice Count] )

Project Count =
DISTINCTCOUNT ( Projects[ProjectID] )

Completed Projects =
CALCULATE (
    [Project Count],
    Projects[Status] = "Completed"
)

Project Completion Rate =
DIVIDE ( [Completed Projects], [Project Count] )
```

Confirm that the chosen date relationship and filter context match the intended meaning before using time-based measures. Add final measure names, definitions, formats, and validation notes to the documentation once checked in Power BI.

## Dashboard pages

The report has five pages:

1. **Executive Overview** — high-level summary of business performance. Confirm the displayed headline KPIs and default date range in the PBIX.
2. **Revenue & Service Performance** — review revenue and service-level patterns. Confirm revenue definitions, trends, and service comparisons.
3. **Project Delivery** — examine project workload and delivery. Confirm status categories, completion logic, and any timing measures.
4. **Client Analytics** — explore client-level distribution and engagement. Confirm which client dimensions and measures are shown.
5. **Resource & Employee Utilization** — review employee and assignment patterns. Confirm utilization denominator, capacity assumptions, and the treatment of overlapping assignments.

## Key insights

**To be completed only after checking actual report values.** No numeric findings are asserted in this README. Review the PBIX with its intended filters and date range, record the relevant values, and state the scope and period for each finding. Suggested prompts:

- Which service contributes the largest share of the selected revenue measure, and for what period?
- How many projects are completed, active, delayed, or otherwise categorized under the report's actual status definitions?
- Which client or client segment has the greatest activity in the selected period?
- How is assignment load distributed across employees, and what capacity definition supports any utilization claim?
- What feedback pattern is visible, and how many feedback records support it?

## Setup and use

1. Install or open a compatible version of Power BI Desktop and SQL Server (or SQL Server Express) with SQL Server Management Studio or another SQL client.
2. Create or restore the `ITServicesBI` database using the project's SQL scripts or supplied database backup. The actual source files and restore procedure are not included in this documentation yet.
3. In Power BI Desktop, open the project `.pbix` file from: **`[LOCAL PATH TO PBIX]`**.
4. If prompted, update the SQL Server connection in Power Query or Data source settings:
   - Server: **`[LOCAL SERVER OR INSTANCE]`**
   - Database: **`ITServicesBI`**
   - Authentication: **`[SELECT YOUR CONFIGURED AUTHENTICATION METHOD]`**
5. Do not put passwords, tokens, or other credentials in this README, source control, screenshots, or shared files. Use your local approved authentication method and Power BI credential settings.
6. Apply changes and refresh. Resolve any schema or permission errors against the local database.
7. Check slicers, page filters, date range, and a sample of totals against SQL before interpreting or sharing report findings.

No server name, file path, username, or password is assumed here. Replace the bracketed placeholders with environment-specific, non-secret details only where appropriate.

## Limitations

- The dataset is synthetic and may not reflect real-world distributions, seasonality, costs, service demand, staffing capacity, or customer behavior.
- Dashboard results depend on the chosen definitions, relationships, filters, and refresh state.
- Revenue should not be interpreted as profit, cash collected, or recognized revenue unless the source fields and business rules explicitly support that interpretation.
- Employee utilization requires a defined capacity denominator and treatment of leave, part-time schedules, and overlapping assignments; assignment counts alone do not establish utilization.
- No actual report values or verified business findings are included in this template.
- This is an analytical portfolio/demo project, not a production operational system or a source of real company records.

## Suggested repository structure
```
IT-Services-BI-Dashboard/
├── README.md
├── docs/
│   ├── [PROJECT_DOCUMENTATION.md](https://github.com/sandeep-sandy123/IT-Services-Business-Intelligence-AI-Assisted-Analytics-Dashboard/blob/main/PROJECT_DOCUMENTATION.md)
│   ├── data_dictionary.md
│   └── screenshots/
├── powerbi/
│   └── ITServicesBI_Dashboard.pbix
├── sql/
│   ├── schema/
│   ├── data_or_seed_scripts/
│   └── validation_queries/
└── assets/
    └── report-preview.png
```

Only include files you have permission to share. Avoid committing credentials, private data, or a database backup unless its distribution is appropriate. If the PBIX contains local paths or credentials, clear or parameterize them before sharing.

## Next steps

1. Open the PBIX and verify each page, measure, filter, and data source against this README.
2. Add a report screenshot and a data dictionary with actual field names and definitions.
3. Validate key totals against SQL using the same filters and date scope as the report.
4. Fill in the Key insights section with observed values, period, and filter context.
5. Replace setup placeholders with your local non-secret connection details or a clear instruction for configuring them.
6. Review the PBIX and repository for sensitive information before sharing or publishing.

## Documentation

See [`docs/PROJECT_DOCUMENTATION.md`][(docs/PROJECT_DOCUMENTATION.md)](https://github.com/sandeep-sandy123/IT-Services-Business-Intelligence-AI-Assisted-Analytics-Dashboard/blob/main/PROJECT_DOCUMENTATION.md) for a fuller project record and fill-in checklist.
