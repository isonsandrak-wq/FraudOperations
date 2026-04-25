# Fraud Operations – Productivity & Loss Early Warning

This repository contains two essential SQL queries for fraud operations managers:

1. **Investigator daily productivity with benchmarks** – measures individual case closure rates against team averages.
2. **Fraud Loss Early Warning (ERW)** – tracks weekly loss trends by fraud type to spot emerging threats.

Together, they help operations leaders improve efficiency, maintain SLAs, and detect loss spikes before they become crises.

---

## Query 1: `investigator_daily_productivity_with_benchmarks.sql`

### What it does
- Calculates for each investigator: **total cases closed**, **days worked**, and **average cases closed per day**.
- Computes the **team‑wide average** of cases closed per day (the benchmark).
- Shows the **difference** between each investigator’s average and the team average.

## Business Impact

- **Improved SLA adherence** – By identifying bottlenecks and high‑volume investigators, workload can be redistributed more evenly.
- **Data‑driven coaching** – Managers can focus on investigators who fall below the team average with specific, objective metrics.
- **Resource planning** – Forecast staffing needs based on average case closure rates across the team.

**Example output:**

| Investigator | Avg Cases / Day | Team Avg | vs Team Avg |
|--------------|----------------|----------|--------------|
| Jordan S.    | 12.4           | 10.2     | +2.2 ▲       |
| Taylor M.    | 9.8            | 10.2     | -0.4 ▼       |
| Alex R.      | 14.1           | 10.2     | +3.9 ▲       |
| Casey L.     | 8.7            | 10.2     | -1.5 ▼       |

**Business impact:**  
- Data‑driven coaching conversations  
- Balanced workload distribution  
- Improved SLA adherence  

---

## Query 2: `Fraud_Loss_ERW.sql`

### What it does
- Aggregates fraud losses by **week** and **fraud type** (synthetic ID, ATO, identity theft, etc.).
- Calculates:
  - Total loss for each fraud type that week  
  - Total loss for all types that week  
  - Percentage contribution of each type to the weekly total  
  - Average loss per type that week (for comparison)

### Why it matters
Fraud patterns shift quickly. A sudden increase in a single fraud type (e.g., ATO) can go unnoticed if you only look at overall loss. This query provides **early warning** by showing you which fraud type is growing as a percentage of total loss, week over week. The `percentage_of_week_total` and comparison to the weekly average help leaders decide where to focus rule tuning, training, or new detection.

**Example output:**

| week_start | fraud_type_label       | loss_this_type | loss_all_types | pct_of_week | avg_loss_per_type |
|------------|------------------------|----------------|----------------|-------------|-------------------|
| 2025-03-03 | Account Takeover       | $45,000        | $150,000       | 30.0%       | $25,000           |
| 2025-03-10 | Synthetic Identity     | $80,000        | $180,000       | 44.4%       | $30,000           |
| 2025-03-17 | Account Takeover       | $95,000        | $200,000       | 47.5%       | $33,000           |

**Business impact:**  
- Early detection of fraud type spikes  
- Objective data for rule or strategy adjustments  
- Better resource allocation (e.g., shift investigators to high‑growth fraud types)  

---

## How to Use These Queries

1. Clone this repository.
2. Update table/column names to match your case management and loss data.
3. Run the queries in Databricks, Snowflake, PostgreSQL, or any SQL engine.
4. For the productivity query, schedule weekly runs to track improvement over time.
5. For the loss early warning query, review results weekly or make one you review daily and ahre with leadership to spot emerging fraud trends.


*These queries were developed for use during my SQL Saturdays classes and work in Databricks SQL Spark.*
