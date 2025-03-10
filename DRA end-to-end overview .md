DRA Project - End-to-End Overview

Based on the codebase analysis and functions in ara_utils.py, here is a detailed end-to-end understanding of the DRA (Data Reporting & Analytics) project.


---

1. Business Use Case

What is this project about?

The DRA (Data Reporting & Analytics) project is designed to aggregate, process, and generate financial and operational reports for trading desks and risk management teams.
It retrieves data from multiple databases, performs data transformations, and outputs structured PDF reports.

Who is going to use it?

Trading Desk Managers: To monitor financial performance (PnL, risk exposure, supervisory alerts).

Risk Management Teams: To track breaches, limits, IPV valuations, and NPR approvals.

Regulatory Compliance Teams: To ensure policies (PnP) and operational risks (Ops Loss) are managed.

Auditors & Supervisors: To review supervisory alerts, trader activity, and policy adherence.



---

2. Business Requirements

What are the requirements?

The DRA system needs to:

1. Aggregate data from multiple databases.


2. Standardize & transform the data for analysis.


3. Generate detailed financial & risk reports.


4. Visualize key metrics (charts, tables).


5. Allow automated reporting via PDF generation.




---

3. Solution Approach

How is the requirement addressed?

The system retrieves trading, financial, risk, and operational data.

It processes & transforms the data into a structured format.

Finally, ara_report.py generates a PDF report with:

Financial charts (PnL, Limits, Exposures).

Risk metrics (VaR, DV01, Stress Tests).

Operational summaries (Traders, Tasks, Alerts).




---

4. Tools & Technologies Used

What are the tools utilized?


---

5. Databases Used & Content Structure

Which databases are used, and what data do they store?


---

6. Data Processing & Transformation

How is the data transformed?

Each function retrieves raw data from databases and performs transformations before passing it to ara_report.py.
Below are some key data transformations applied:

1️⃣ Financial Data (getFinancials)

Input (Raw Data from GFC_PROD)
| Month | Source | Value  | |-------|--------|--------| | Jan-24 | Income | 100000 | | Jan-24 | Asset  | 500000 |

Transformations

Converts GL_PERIOD to 'Month'

Categorizes Source into Income, Assets, Liabilities

Computes rolling averages for trend analysis.


Output (Processed Data) | Month | Revenue | Assets  | |-------|---------|---------| | Jan-24 | 100000 | 500000  |


---

2️⃣ Risk Exposure Data (getLimits)

Input (Raw Data from audit_automation_prod)
| Desk  | Exposure | Limit Type | |------|----------|------------| | FI   | 100000   | DV01       |

Transformations

Filters exposures exceeding limits.

Aggregates maximum exposures.


Output (Processed Data) | Desk  | Max Exposure | Limit Type | |------|-------------|------------| | FI   | 120000      | DV01       |


---

3️⃣ Supervisory Alerts (getSupervisoryAlerts)

Input (Raw Data from ficc_supervisory_prod)
| Desk  | Exception Rule | Alert Date | |------|---------------|------------| | Equities | Rule A | 2024-03-01 |

Transformations

Counts alerts per desk.

Computes percentage change in alerts over time.


Output (Processed Data) | Desk  | Alerts | Change (%) | |------|--------|------------| | Equities | 10     | +5%        |


---

7. Report Generation

How is the solution implemented?

1. Data Fetching:

Each function queries different databases.

Data is transformed & structured.



2. Data Processing & Formatting:

Converts raw data into structured tables.

Computes rolling averages, trend analysis, alerts tracking.



3. PDF Report Generation (ara_report.py):

Header & Footer → Adds report title, date, branding.

Financial Charts → Revenue, PnL, Asset allocation.

Risk Metrics → Market VaR, DV01, IPV valuations.

Supervisory Alerts → Count of violations, alerts.




Final Report Output (Example)

===========================
DRA Financial Report - March 2024
===========================
1. Revenue: $1,000,000 (+10% MoM)
2. Market Risk: Exposure within limits
3. Supervisory Alerts: 5 Violations (↓2%)


---

8. Final Summary


---

This covers the end-to-end working of the DRA Project in detail.
Let me know if you need more insights or refinements! 🚀

