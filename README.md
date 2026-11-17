# Bengaluru EV Charging Network: Tata Power Project 01

An analysis of the Bengaluru public EV charging network: how it performs today, who uses it, where capacity is missing, and which of the 98 proposed expansion projects are worth building.

- **Data window:** 11 Aug to 8 Nov 2024 (about 90 days)
- **Input file:** `Tata_Power_Project_01.xlsx`
- **Deliverables:** an insights summary (PDF) and a detailed report (PDF)

---

## Project goals

1. Measure network performance: sessions, energy, revenue and utilisation.
2. Understand demand by time of day, income tier and operator.
3. Profile customers by battery size and income tier.
4. Find the gap between existing plugs and projected demand, district by district.
5. Rank the proposed projects by payback and ROI, and recommend where to invest first.

---

## Headline findings

| Area | Finding |
| --- | --- |
| Scale | 114,000 sessions, 28.6 lakh kWh, Rs 4.97 crore revenue, 65 stations, 390 plugs, 8,000 customers |
| Demand | Flat at about 1,280 sessions a day; every plug handles 272 to 310 sessions (no hotspots) |
| Time of day | 50% of sessions start 08:00 to 16:00; a daytime hour carries about 2.5x a night hour |
| Pricing | Revenue is driven by tariff tier (Rs 13.5, 18.0, 22.5 per kWh), not by traffic |
| Operators | Tata Power has the lowest revenue per kWh (Rs 16.61): only 1 of 13 stations is in a High-tier district, versus 3 for each rival |
| Customers | Owners of 60+ kWh cars are 12% of customers but 26% of revenue |
| Capacity gap | 390 of 1,067 projected plugs exist (37% coverage); six districts hold 61% of the 677-plug gap |
| Investment | 54 High-priority AC projects use 36% of CAPEX and give 59% of EBITDA (about 2.6 years payback); 36 of 37 Low-priority projects are DC chargers with negative average ROI |

---

## Data description

The workbook has six data sheets plus dashboard sheets.

| Sheet | Rows | Columns | Purpose |
| --- | --- | --- | --- |
| `charging_sessions` | 114,000 | `session_id`, `customer_id`, `station_id`, `session_start_time`, `kwh_charged`, `cost_per_kwh`, `total_cost`, `Month`, `Month Name`, `Year` | One row per charging session |
| `charging_stations` | 65 | `station_id`, `district_name`, `income_tier`, `operator_name`, `plugs_count`, `latitude`, `longitude` | Station master data |
| `customers` | 8,000 | `customer_id`, `income_tier`, `car_model`, `battery_capacity_kwh`, `Battery Band` | Customer master data |
| `districts` | 18 | `district_name`, `income_tier`, `projected_evs`, `projected_plugs`, `projected_regular_customers` | District demand projection |
| `roi_bengaluru_districts` | 98 | `Project_ID`, `District`, `Charger_Type`, `Total_CAPEX_Lakh`, `Annual_EBITDA_Lakh`, `Payback_Period_Yrs`, `5yr_ROI_Pct`, `Priority_Tier`, and 18 more | Proposed projects and their economics |
| `PivotTable`, `Dashboard 1` to `4` | n/a | n/a | Pivot summaries and dashboards |

**Relationships:** `charging_sessions.station_id` joins to `charging_stations`, and `charging_sessions.customer_id` joins to `customers`. District names link stations, projections and projects.

---

## Method

1. Joined sessions to stations and customers (all 114,000 sessions matched a station).
2. Recomputed totals and ratios from the raw sheets and cross-checked them against the workbook's pivot values.
3. Compared per-plug utilisation across stations, tiers and operators.
4. Computed the plug gap as projected plugs minus existing plugs per district.
5. Summarised the ROI model by charger type, priority tier, district and site type. Where the workbook uses simple averages across projects, portfolio-level figures were added.

**Assumptions:**

- One charging gun is treated as one plug when comparing the project pipeline to the plug gap.
- Revenue is `kwh_charged x cost_per_kwh`; the tariff maps exactly to the station district's income tier.

---

## Limitations

- About 90 days of data: no seasonality, growth or churn view. August and November are partial months.
- Patterns are very uniform across plugs, operators and weekdays, which suggests modelled data. Treat findings as directional.
- ROI, payback and tariff figures come from the workbook's ROI model and were not independently validated.

---

## Deliverables

| File | Description |
| --- | --- |
| `Tata_Power_EV_Charging_Insights.pdf` | 7-page insights summary with charts |
| `Tata_Power_EV_Charging_Report.pdf` | 7-page detailed report: method, findings, recommendations, risks, next steps |
| `build.py` | Generates the charts and the insights PDF |
| `build_report.py` | Generates the detailed report PDF (reuses the charts from `build.py`) |

---

## Reproducing the outputs

**Requirements:** Python 3.10+ with `pandas`, `openpyxl`, `matplotlib`, `reportlab` and `Pillow`, plus the DejaVu Sans fonts (used so the PDFs render properly).

```bash
pip install pandas openpyxl matplotlib reportlab pillow
```

1. Put `Tata_Power_Project_01.xlsx` where the scripts expect it, or change the `F` path at the top of `build.py`.
2. Run `python build.py` to create the charts in `charts/` and the insights PDF.
3. Run `python build_report.py` to create the detailed report PDF.

Both scripts write to `/mnt/user-data/outputs/` by default. Change the `OUT` variable in each script to write elsewhere.

---

## Recommendations in brief

1. Build the 54 High-priority AC projects first.
2. Re-underwrite or defer the DC fast and ultra-fast projects.
3. Redesign Koramangala, Indiranagar and Whitefield proposals around AC 22 kW chargers.
4. Introduce time-of-use pricing.
5. Improve Tata Power's station mix toward High-tier districts.
6. Target the premium EV segment with loyalty offers.
7. Pilot a tariff increase in Low-Mid districts.

---

## Suggested next steps

- Confirm the gun-to-plug assumption and finalise the High-priority shortlist by district.
- Stress-test DC project economics (tariff, utilisation, subsidy).
- Pilot time-of-use pricing at several stations.
- Collect at least 12 months of session data.
"# Tata-Power" 
"# Tata-Power" 
