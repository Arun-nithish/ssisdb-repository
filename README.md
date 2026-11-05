# SSISDB Dashboard

Monitor SSIS Catalog (SSISDB) executions: success rate, durations, slowest packages, step-level Gantt and errors.

**Live demo (sample data):** open `index.html`, or enable GitHub Pages (Settings > Pages > Deploy from branch > `main` / root).

## What's inside
| Path | Purpose |
|---|---|
| `sql/01_dashboard_views.sql` | Read-only views (`dashboard.*`) over `catalog.*` tables |
| `powerbi/queries.pq` | Power Query M for each table |
| `powerbi/measures.dax` | DAX measures (success rate, durations, errors) |
| `index.html` | Standalone demo of the dashboard layout with sample data |

## Setup
1. Run `sql/01_dashboard_views.sql` against your SSIS server, then grant `SELECT` on the `dashboard` schema to the reporting user.
2. In Power BI Desktop: Get data > Blank Query, paste each query from `powerbi/queries.pq`. Create text parameters `ServerName` and `DatabaseName`.
3. Add relationships: `Executions[execution_id]` 1 -> * `ExecutableStats[execution_id]` and `Errors[execution_id]`.
4. Add the measures from `powerbi/measures.dax`.
5. Suggested pages: Summary, Packages, Execution (Gantt), Errors, Over time.
6. Export as `.pbit` (File > Export > Power BI template) and add it to the repo. Never commit a `.pbix` containing real data or server names.

## Roadmap
- Row counts from data-flow messages (`dashboard.RowCounts`)
- Currently running packages page
- Package type grouping (`PackageTypes` query)
