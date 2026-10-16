# IT Services Business Intelligence & AI-Assisted Analytics Dashboard

An end-to-end Power BI portfolio project for exploring the operational and financial performance of a fictional IT services business. The project combines a SQL Server data source, Power Query preparation, a Power BI data model, DAX measures, and a five-page interactive report.

> **Data notice:** This project uses synthetic data for demonstration and learning. It is not real customer, employee, financial, or operational data, and it must not be presented as proprietary data from Xscade or any other real organization.

## Project overview

The dashboard brings together client, service, project, staffing, invoice, feedback, and calendar data. It is designed to help users review revenue and service performance, project delivery, client patterns, and resource utilization in one report.

### Business objectives

- Monitor invoice revenue and service performance over time.
- Review project delivery status, timelines, and workload.
- Understand client mix and engagement patterns.
- Explore employee assignments and resource utilization.
- Bring operational and financial views together to support analysis.

These are intended uses of the dashboard. Confirm the exact definitions and available visuals in the PBIX before treating any metric as a formal business KPI.

## Dashboard preview

Adding the screenshot here:

### ![executive-overview](https://github.com/sandeep-sandy123/IT-Services-Business-Intelligence-AI-Assisted-Analytics-Dashboard/blob/main/01-executive-overview.png)

### ![revenue-service-performance](https://github.com/sandeep-sandy123/IT-Services-Business-Intelligence-AI-Assisted-Analytics-Dashboard/blob/main/02-revenue-service-performance.png)

### ![project-delivery](https://github.com/sandeep-sandy123/IT-Services-Business-Intelligence-AI-Assisted-Analytics-Dashboard/blob/main/03-project-delivery.png)

### ![client-analytics](https://github.com/sandeep-sandy123/IT-Services-Business-Intelligence-AI-Assisted-Analytics-Dashboard/blob/main/04-client-analytics.png)

### ![resource-employee-utilization](https://github.com/sandeep-sandy123/IT-Services-Business-Intelligence-AI-Assisted-Analytics-Dashboard/blob/main/05-resource-employee-utilization.png)

---
## Tools and technologies

- Microsoft SQL Server — database and source tables
- Power Query — data import, cleanup, and transformation
- Microsoft Power BI Desktop — data modeling, DAX, and report visuals
- DAX — measures and calculated logic

## Dataset at a glance

The database is named `ITServicesBI` and contains eight tables. Counts below are the supplied project counts; row counts may differ if the local database has changed.

| Table | Rows | Purpose |
|---|---:|---|
| `Client` | 80 | Client entities and client attributes |
| `Services` | 8 | Service categories or offerings |
| `Projects` | 220 | Project records and delivery attributes |
| `Employees` | 45 | Employee or resource records |
| `Project_Assignments` | 709 | Employee-to-project assignment records |
| `Invoices` | 446 | Invoice or billing records |
| `Customer_Feedback` | 79 | Customer feedback records |
| `Calendar` | 2025–2026 | Date dimension covering calendar years 2025 and 2026; row count not supplied |

The model screenshot uses the singular name `Client`. Confirm whether the source database also uses that name; earlier project notes listed it as `Clients`.

The project uses synthetic data. Confirm column names, key fields, date coverage, and row counts against the database before reproducing the model.

## Data preparation and modeling

The reported workflow is:

**SQL Server → Power Query → Power BI model → DAX measures → report pages**

Typical preparation tasks include checking data types, trimming and standardizing text, reviewing nulls and duplicates, and confirming key relationships. Document only the transformations actually present in the Power Query steps.

The model screenshot shows relationships connecting clients, services, calendar dates, projects, project assignments, employees, invoices, and customer feedback. Check the relationship properties in Power BI to confirm the exact join columns, filter directions, and date relationships.

## Dashboard pages

The report contains five pages:

1. **Executive Overview** — high-level summary of business performance.
2. **Revenue & Service Performance** — review revenue and service-level patterns.
3. **Project Delivery** — examine project workload and delivery.
4. **Client Analytics** — explore client-level distribution and engagement.
5. **Resource & Employee Utilization** — review employee and assignment patterns.

Confirm the displayed visuals, slicers, and metric definitions in the PBIX before describing specific findings.

## KPI and DAX examples

The formulas below are illustrative patterns only. They do not confirm that measures with these names or definitions exist in the project. Adjust table and column names and business rules to match the actual model.

```DAX
Total Revenue =
SUM ( Invoices[InvoiceAmount] )

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
Confirm what “revenue” means in the report and whether the project status field and values match these examples. A sum of invoices is not automatically equivalent to cash collected or recognized revenue.
Key insights
Fill in this section only after checking actual report values. No numeric findings are asserted here.
For each finding, record the value, reporting period, relevant filters, and how you validated it. Questions to consider:
- Which service contributes the largest share of the selected revenue measure?
- How many projects fall into each status shown in the report?
- Which clients have the greatest activity in the selected period?
- How are assignments distributed across employees?
- What feedback patterns appear, and how many feedback records support them?
Setup and use
1. Install or open a compatible version of Power BI Desktop and SQL Server (or SQL Server Express).
2. Create or restore the ITServicesBI database using the project’s SQL scripts or supplied database backup.
3. Open the project .pbix file from: [LOCAL PATH TO PBIX].
4. If prompted, update the SQL Server connection:
   - Server: [LOCAL SERVER OR INSTANCE]
   - Database: ITServicesBI
   - Authentication: [SELECT YOUR CONFIGURED AUTHENTICATION METHOD]
5. Apply changes and refresh the report. Resolve any source or permission errors against your local database.
6. Check slicers, page filters, date range, and sample totals against SQL before interpreting report findings.
No server name, file path, username, or password is assumed here. Do not put passwords, tokens, or other credentials in this README or source control. Use your local authentication settings.
Limitations
- The dataset is synthetic and may not reflect real-world distributions, seasonality, costs, service demand, staffing capacity, or customer behavior.
- Dashboard results depend on the chosen definitions, relationships, filters, and refresh state.
- Revenue should not be interpreted as profit, cash collected, or recognized revenue unless the source fields and business rules support that interpretation.
- Employee utilization requires a defined capacity denominator and treatment of leave, part-time schedules, and overlapping assignments. Assignment counts alone do not establish utilization.
- This is an analytical portfolio/demo project, not a production operational system or a source of real company records.
Suggested repository structure
IT-Services-BI-Dashboard/
├── README.md
├── docs/
│   ├── PROJECT_DOCUMENTATION.md
│   └── screenshots/
│       ├── 01-executive-overview.png
│       ├── 02-revenue-service-performance.png
│       ├── 03-project-delivery.png
│       ├── 04-client-analytics.png
│       └── 05-resource-employee-utilization.png
├── powerbi/
│   └── ITServicesBI_Dashboard.pbix
├── sql/
│   ├── schema/
│   ├── data_or_seed_scripts/
│   └── validation_queries/
└── assets/
    └── report-preview.png
Only include files you have permission to share. Avoid committing credentials, private data, or database backups that should not be distributed. Check the PBIX for local paths or credentials before sharing.
Next steps
1. Verify the table names, model relationships, measures, and visuals against the PBIX and database.
2. Add the five page screenshots to docs/screenshots/.
3. Add the Executive Overview screenshot as assets/report-preview.png.
4. Replace the setup placeholders with your local non-secret connection details or instructions.
5. Fill in Key insights with observed values, date range, and filter context.
6. Review the files for sensitive information and keep the synthetic-data disclaimer before sharing.

You can also download the editable file here: [README.md](C:\Users\user\Documents\Codex\2026-10-16\referenced-chatgpt-conversation-this-is-an\outputs\README.md).
