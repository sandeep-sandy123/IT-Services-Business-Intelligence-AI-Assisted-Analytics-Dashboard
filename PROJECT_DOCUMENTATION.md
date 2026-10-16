# Project Documentation

## IT Services Business Intelligence & AI-Assisted Analytics Dashboard

**Document status:** Project documentation template based on supplied project facts. Validate all implementation-specific statements against the saved Power BI file and local SQL Server database before distribution.

## 1. Project purpose

This Power BI project demonstrates how an IT services business could bring operational and financial records together for interactive analysis. It uses a synthetic dataset in SQL Server database `ITServicesBI`, prepares data with Power Query, models the data in Power BI, and presents analysis across five report pages.

The intended audience is a portfolio reviewer, analyst, or business stakeholder who needs a concise view of revenue, services, project delivery, clients, and resource assignments. The dashboard is an analytical demonstration and is not a production system.

## 2. Data and provenance

All project data is synthetic. It must not be described as real company data, customer records, employee records, or proprietary Xscade data. If the project was created in an internship or company context, distinguish the fictional/demo dataset from any real organization clearly in presentations and repository materials.

### Tables supplied

| Table | Supplied volume | Expected subject area (verify against schema) |
|---|---:|---|
| `Clients` | 80 rows | Clients |
| `Services` | 8 rows | Service catalog or service categories |
| `Projects` | 220 rows | Projects and delivery attributes |
| `Employees` | 45 rows | Employees/resources |
| `Project_Assignments` | 709 rows | Project-resource assignments |
| `Invoices` | 446 rows | Billing/invoice records |
| `Customer_Feedback` | 79 rows | Customer feedback |
| `Calendar` | Covers 2025–2026 | Date dimension; number of rows not supplied |

### Data dictionary to complete

For each actual field, document its name, type, description, key role, allowed values, null behavior, and source. At minimum, identify primary keys, foreign keys, date fields, amount fields, status fields, and any columns used in measures. Do not infer field names from the illustrative DAX below.

## 3. Data preparation workflow

The reported preparation tools are SQL Server and Power Query. Record the actual applied steps from the PBIX in this section:

| Step | Actual implementation to document |
|---|---|
| Source connection | Server/instance placeholder, database `ITServicesBI`, tables or views loaded |
| Type handling | Date, whole number, decimal/currency, text, and Boolean conversions |
| Quality checks | Nulls, duplicates, invalid keys, out-of-range dates, unexpected statuses |
| Transformations | Exact Power Query steps, renames, filters, derived columns, and rationale |
| Load behavior | Import or DirectQuery mode, refresh expectations, and any incremental refresh |

Do not record secrets or personal credentials. If the PBIX uses Import mode, specify the date of the latest successful refresh when sharing a release.

## 4. Data model

Document the actual model rather than relying on table names alone. Add a model screenshot or diagram and complete this relationship inventory:

| From table/column | To table/column | Cardinality | Filter direction | Active? | Purpose |
|---|---|---|---|---|---|
| `[fill from model]` | `[fill from model]` | `[verify]` | `[verify]` | `[verify]` | `[describe]` |

Confirm whether `Calendar` is marked as a date table and identify which date column each time-based visual or measure uses. Where there are multiple date roles (for example invoice date and project start/end dates), explain which relationship is active and how alternate dates are selected.

## 5. Measures and KPI definitions

Use this register for the actual measures in the PBIX. Specify the business definition, DAX, formatting, expected grain, and a validation query or manual reconciliation for every headline metric.

| Measure | Business definition | Format | Validation / notes |
|---|---|---|---|
| `[actual measure]` | `[exact numerator, filters, exclusions, time basis]` | `[format]` | `[SQL or visual check]` |

### Illustrative DAX patterns only

These examples assume columns that may not exist in the supplied model. Replace names and business rules, then validate results before use.

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

For each actual measure, verify how blank amounts, cancelled invoices, duplicates, status spelling, date filters, and relationships affect the result. A sum of invoices is not automatically equivalent to collected or recognized revenue. A count of assignments is not a utilization rate unless there is a defensible capacity denominator.

## 6. Report page guide

The project contains these five pages. Add the actual visuals, slicers, and navigation details after checking the PBIX.

| Page | Intended question | Actual visuals / controls to record |
|---|---|---|
| Executive Overview | What is the selected high-level business picture? | `[KPIs, charts, slicers, default period]` |
| Revenue & Service Performance | How do revenue and service results vary? | `[measure definitions, trends, comparisons]` |
| Project Delivery | What is the project portfolio and delivery status? | `[status logic, dates, workload visuals]` |
| Client Analytics | Which clients or groups drive activity? | `[client measures, segmentation, filters]` |
| Resource & Employee Utilization | How are assignments and resources distributed? | `[capacity assumption, assignment logic, visuals]` |

Record interactions that matter to interpretation, including cross-filtering, drill-through, tooltip pages, bookmarks, and synced slicers.

## 7. Findings and interpretation

**No findings have been verified for this document. Complete this section only after reviewing the actual report values.** For each observation, capture the measure definition, value, reporting period, filter context, and a source check. Avoid claims about trends or causes unless the report and data support them.

| Finding | Report value and period | Filters / segment | Validation |
|---|---|---|---|
| `[complete after report review]` | `[value and dates]` | `[context]` | `[source check]` |

## 8. Local setup and refresh

1. Ensure SQL Server is running and the synthetic project database `ITServicesBI` has been created or restored from the project's actual scripts/backup.
2. Open `[LOCAL PATH TO PBIX]` in Power BI Desktop.
3. Configure the data source using your local SQL Server or instance: `[LOCAL SERVER OR INSTANCE]`.
4. Select the database `ITServicesBI` and the authentication method configured on that machine. Credentials are intentionally not included in this document.
5. Refresh the model and inspect errors. If the source schema differs, update the queries and model deliberately, then revalidate measures and visuals.
6. Compare representative report totals with SQL using matching date and filter conditions.
7. Record the Power BI Desktop version, storage mode, last refresh date, and any required drivers or gateway configuration here: `[complete]`.

Exact connection strings and local paths are environment-specific. Store them in local Power BI settings or appropriately protected configuration, not in version control. Do not commit passwords, tokens, or private data.

## 9. Limitations and responsible presentation

- Synthetic data supports demonstration but cannot establish the performance of a real business or its customers and employees.
- Row counts and values may change as the dataset is regenerated or modified.
- Measures are meaningful only when their fields, filters, date relationships, and business definitions are documented.
- Utilization, profitability, revenue recognition, customer satisfaction, and delivery performance each require precise definitions; do not infer them from similarly named fields alone.
- This project is not a forecast, causal analysis, audited financial statement, or production operational platform unless separately designed and validated for those purposes.
- Do not imply that this synthetic dataset is sourced from or represents Xscade or another real organization.

## 10. Suggested repository layout

```text
IT-Services-BI-Dashboard/
├── README.md
├── docs/
│   ├── PROJECT_DOCUMENTATION.md
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

Adjust this tree to match the files that actually exist. Avoid adding generated backups or data dumps that should not be distributed.

## 11. Completion checklist

- [ ] Confirm every table, row count, field, and relationship against SQL Server and the PBIX.
- [ ] Document the actual Power Query steps and storage/refresh mode.
- [ ] Replace illustrative DAX with verified measures and definitions.
- [ ] Validate key totals with SQL under matching date and filter context.
- [ ] Describe actual visuals and interactions on all five pages.
- [ ] Add only findings observed in the report and include period and filter context.
- [ ] Add a data dictionary and a clear report screenshot if appropriate.
- [ ] Replace local path/server placeholders without including secrets.
- [ ] Review for private information and preserve the synthetic-data disclaimer before sharing.
