# 🚛 Logistics Operations Dashboard — Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?style=flat-square&logo=powerbi)
![DAX](https://img.shields.io/badge/DAX-Measures-green?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)
![Records](https://img.shields.io/badge/Loads-85%2C410-blue?style=flat-square)
![Period](https://img.shields.io/badge/Period-2022--2024-purple?style=flat-square)

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Dashboard Pages](#dashboard-pages)
- [Dataset Information](#dataset-information)
- [Project Objectives](#project-objectives)
- [Tools & Technologies](#tools--technologies)
- [Data Cleaning & Preparation](#data-cleaning--preparation)
- [Data Model & Relationships](#data-model--relationships)
- [DAX Measures](#dax-measures)
- [Key Metrics Summary](#key-metrics-summary)
- [Key Insights](#key-insights)
- [Business Recommendations](#business-recommendations)
- [Project Workflow](#project-workflow)
- [Folder Structure](#folder-structure)
- [Skills Demonstrated](#skills-demonstrated)
- [Results Summary](#results-summary)
- [Future Improvements](#future-improvements)
- [Conclusion](#conclusion)

---

## 📌 Project Overview

This project delivers a fully interactive **4-page Power BI dashboard** analysing the end-to-end operations of a US-based trucking and logistics company. The analysis covers 85,410 loads, 150 active drivers, 200 customers, and 122 million miles of freight movement across a three-year period from 2022 to 2024.

### The Business Problem

Trucking operations generate data across multiple disconnected systems — loads, trips, fuel purchases, maintenance records, delivery events, and safety incidents. Without a unified analytical view, operations managers cannot see which routes are profitable, which drivers are underperforming, where safety incidents are concentrated, or which customers are generating the most value. Decisions get made on intuition rather than evidence.

### Why This Analysis Matters

With $298.6 million in total revenue and only a 55.67% on-time delivery rate, this business is generating strong top-line numbers while quietly experiencing a service quality crisis. Nearly half of all 85,410 deliveries arrived late. The dashboard surfaces these issues and provides the granularity needed to act on them.

### Objective

To connect 14 tables of operational logistics data into a single Power BI model, build a suite of DAX measures covering revenue, profitability, safety, and service quality, and deliver a four-page interactive dashboard that answers the most critical business questions across operations, driver management, fleet safety, and customer analysis.

---

## 📊 Dashboard Pages

### Page 1 — Overview
The executive summary page showing headline KPIs, top 10 customers by revenue, customer type revenue split, monthly incident trend, fleet utilization gauge, vehicle damage cost by incident type, average revenue per load, and a monthly financial summary table.

![Overview Dashboard](images/LOGIS.png)

---

### Page 2 — Drivers & Route Performance
Covers on-time delivery rate, late delivery count, active driver count, profit per driver, booking type split (Dedicated / Contract / Spot), total loads delivered by driver, driver experience vs incident rate, and route profit by lane.

![Drivers & Route Performance](images/LOGIS2.png)

---

### Page 3 — Maintenance & Safety
Tracks total damage cost, preventable incident rate, total downtime hours, total maintenance cost, maintenance cost by type, incidents by home terminal, incident type breakdown, and monthly incident trend.

![Maintenance & Safety](images/LOGIS3.png)

---

### Page 4 — Customers Analysis
Analyses total customers, total loads delivered, total revenue, late deliveries by customer, load volume and revenue ranking by customer name, and monthly profit trend.

![Customers Analysis](images/LOGIS1.png)

---

## 🗂 Dataset Information

| Attribute | Details |
|---|---|
| **Total Tables** | 14 connected tables |
| **Total Loads** | 85,410 |
| **Total Customers** | 200 |
| **Active Drivers** | 150 |
| **Total Miles Driven** | 122,159,201 |
| **Period Covered** | January 2022 – December 2024 |
| **Model Type** | Star schema with central Date table |

### Tables in the Data Model

| Category | Tables |
|---|---|
| **Dimensions** | customers, drivers, trucks, trailers, routes, facilities |
| **Facts** | loads, trips, fuel\_purchases, maintenance\_records, delivery\_events, safety\_incidents |
| **Aggregates** | driver\_monthly\_metrics, truck\_utilization\_metrics |

---

## 🎯 Project Objectives

- Measure total revenue, profit, and margin across the 3-year operation
- Identify which customers and routes generate the highest revenue and profit
- Evaluate on-time delivery performance against industry benchmarks
- Analyse driver performance across loads delivered, revenue, and safety incidents
- Assess fleet utilisation and average fuel efficiency (MPG)
- Break down maintenance costs by type to support budget planning
- Identify preventable safety incidents and their financial impact
- Surface which home terminals have the highest incident concentration
- Measure route profitability by lane to guide pricing and load acceptance decisions
- Track monthly profit trends to identify seasonal patterns

---

## 🛠 Tools & Technologies

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Data modelling, DAX measures, and dashboard development |
| **Power Query (M)** | Data cleaning, type standardisation, and transformation |
| **DAX** | Custom KPIs, calculated measures, and time intelligence |
| **Star Schema** | Relationship modelling across 14 tables |
| **SQL** | Source data validation and cross-table join queries |
| **Excel / CSV** | Source data format |

---

## 🧹 Data Cleaning & Preparation

All cleaning was performed in Power Query before the data entered the Power BI model.

**Removed duplicate records** across all 14 tables to ensure counts and totals were not inflated by repeated rows.

**Fixed data types** on every column — date columns set to Date or Date/Time, revenue and cost columns set to Decimal Number, quantity columns set to Whole Number, and identifier columns set to Text.

**Standardised text columns** including city names, event types, order statuses, and booking types — trimming whitespace and unifying casing so that values matched consistently across tables for reliable grouping and filtering.

**Handled missing values** by column — columns where blank means "not applicable" (such as a driver with no termination date) were left blank, while numeric cost columns were filled with zero where appropriate.

**Created a central Date table** with Year, Quarter, Month Number, Month Name, and Month-Year columns, marked as a Date Table in Power BI and connected to every fact table's date column. This enables all time intelligence measures to work correctly from a single date slicer.

**Built all relationships** in Model view — each fact table linked to its dimensions on matching key columns, all set as one-to-many with single-direction filtering, forming a clean star schema.

**Disabled Auto Date/Time** in Power BI settings to prevent hidden date tables from inflating model size.

---

## 🔗 Data Model & Relationships

The full data model was built in Power BI Model view using a star schema pattern. All 14 tables are connected through clearly defined one-to-many relationships with single-direction filtering, so that every slicer and filter on the dashboard propagates correctly through the model without ambiguity.

### Relationship Diagram

![Data Model & Relationships](images/model_view.png)

### How the Tables Connect

The model is structured around **trips** as the central fact table, since a trip is the atomic operational event that touches almost every other entity — a driver, a truck, a trailer, a load, fuel purchases, delivery events, and safety incidents.

| From (One side) | To (Many side) | Key Column | What it enables |
|---|---|---|---|
| `customers` | `loads` | `customer_id` | Revenue and delivery metrics filtered by customer |
| `routes` | `loads` | `route_id` | Lane profitability analysis |
| `loads` | `trips` | `load_id` | Connecting order data to actual trip execution |
| `drivers` | `trips` | `driver_id` | Driver performance metrics |
| `trucks` | `trips` | `truck_id` | Fleet utilisation and maintenance attribution |
| `trailers` | `trips` | `trailer_id` | Trailer usage analysis |
| `trips` | `fuel_purchases` | `trip_id` | Fuel cost per trip and per lane |
| `trips` | `delivery_events` | `trip_id` | On-time delivery analysis |
| `trips` | `safety_incidents` | `trip_id` | Incident attribution to trip and driver |
| `trucks` | `maintenance_records` | `truck_id` | Maintenance cost and downtime per truck |
| `trucks` | `truck_utilization_metrics` | `truck_id` | Monthly fleet utilisation summaries |
| `drivers` | `driver_monthly_metrics` | `driver_id` | Monthly driver performance aggregates |
| `drivers` | `fuel_purchases` | `driver_id` | Fuel efficiency linked to individual drivers |
| `drivers` | `safety_incidents` | `driver_id` | Safety record per driver |
| `delivery_events` | `facilities` | `facility_id` | Detention and on-time analysis by facility |

### Key Modelling Decisions

**All relationships are one-to-many with single cross-filter direction.** This is the Power BI best practice — bidirectional filtering can cause ambiguous results and circular dependencies in a model with this many tables. Single direction means filter context flows from dimension to fact, which is exactly how analytical queries work.

**The `loads` to `trips` relationship is one-to-one.** Every load has exactly one associated trip in this dataset, making this the join that bridges the commercial layer (customers, revenue, routes) to the operational layer (drivers, trucks, fuel, safety).

**`driver_monthly_metrics` and `truck_utilization_metrics` are pre-aggregated.** They are connected to `drivers` and `trucks` respectively and used for monthly trend analysis without needing to aggregate the raw fact tables — improving report performance significantly.

**`routes` contains a calculated column `Lane`** (visible in the model view as a custom field) used as the denominator in the `Fuel Cost per Lane` measure.

---

## 📐 DAX Measures

All measures were written in Power BI Measure tools and are documented below with their exact formula, the table they live in, the format applied, and an explanation of what each one calculates and why it was built that way.

### Measure Screenshots

The following screenshots show every measure formula as written in Power BI.

**AVG MPG**
![AVG MPG](images/dax_avg_mpg.png)

**Total Miles Driven**
![Total Miles Driven](images/dax_total_miles.png)

**Total Incidents**
![Total Incidents](images/dax_total_incidents.png)

**Fuel Cost per Lane**
![Fuel Cost per Lane](images/dax_fuel_cost_per_lane.png)

**Total Downtime Hour**
![Total Downtime Hour](images/dax_downtime.png)

**Total Maintenance Cost**
![Total Maintenance Cost](images/dax_maintenance_cost.png)

**Total Load Delivered**
![Total Load Delivered](images/dax_total_loads.png)

**Revenue % by Customer Type**
![Revenue % by Customer Type](images/dax_revenue_pct.png)

**Profit Margin %**
![Profit Margin %](images/dax_profit_margin.png)

**Profit per Driver**
![Profit per Driver](images/dax_profit_per_driver.png)

**Late Deliveries**
![Late Deliveries](images/dax_late_deliveries.png)

**Active Drivers**
![Active Drivers](images/dax_active_drivers.png)

**On-time-delivery %**
![On-time-delivery %](images/dax_otd.png)

**Total Customers**
![Total Customers](images/dax_total_customers.png)

---

### Full Measure Reference

| Measure | Table | Format | Formula |
|---|---|---|---|
| AVG MPG | driver\_monthly\_metrics | General | `AVERAGE(driver_monthly_metrics[average_mpg])` |
| Total Miles Driven | trips | Whole Number | `SUM(trips[actual_distance_miles])` |
| TOTAL INCIDENTS | safety\_incidents | Whole Number | `COUNTROWS(safety_incidents)` |
| Fuel Cost per Lane | routes | Whole Number | `DIVIDE(SUM(fuel_purchases[total_cost]), SUM(routes[Lane]))` |
| Total downtime hour | maintenance\_records | General | `SUM(maintenance_records[downtime_hours])` |
| Total Maintenance Cost | maintenance\_records | Currency | `SUM(maintenance_records[total_cost])` |
| Total Load Delivered | loads | Decimal Number | `COUNTROWS(loads)` |
| Revenue % by customer type | loads | General | `DIVIDE([Total Revenue], CALCULATE([Total Revenue], ALL(customers[customer_type])))` |
| Profit Margin% | loads | Percentage | `DIVIDE(routes[Route Profit], [Total Revenue])` |
| Profit per Driver | drivers | General | `DIVIDE(routes[Route Profit], DISTINCTCOUNT(drivers[driver_id]))` |
| Late Deliveries | drivers | Whole Number | `CALCULATE(COUNTROWS(delivery_events), delivery_events[event_type] = "Delivery", delivery_events[on_time_flag] = FALSE)` |
| Active Drivers | drivers | Whole Number | `DISTINCTCOUNT(drivers[driver_id])` |
| On-time-delivery % | driver\_monthly\_metrics | Percentage (2dp) | `DIVIDE(COUNTROWS(FILTER(delivery_events, delivery_events[on_time_flag]=TRUE)), COUNTROWS(delivery_events))` |
| Total Customers | customers | Whole Number | `DISTINCTCOUNT(customers[customer_id])` |

---

### Measure Explanations

**AVG MPG** averages the `average_mpg` field from the `driver_monthly_metrics` table rather than computing it from raw trip fuel gallons. This is intentional — the monthly metrics table holds pre-calculated per-driver MPG which is more reliable than dividing raw gallons against raw miles when some rows may have partial data.

**Total Miles Driven** sums the `actual_distance_miles` column from `trips`, which reflects real kilometres driven rather than the estimated distance on the route plan. Using actual rather than planned distance gives accurate fuel efficiency calculations.

**TOTAL INCIDENTS** is a simple `COUNTROWS` on `safety_incidents`. Because every row in that table is one incident, row count equals incident count. The whole number format confirms this is a count, not a sum of a numeric column.

**Fuel Cost per Lane** divides total fuel spend by the count of lanes using a custom `Lane` calculated column on the `routes` table. This gives an average fuel cost per lane rather than per load, which is useful for comparing lane-level profitability across different route lengths.

**Total downtime hour** sums `downtime_hours` from `maintenance_records`. This is the total number of hours trucks were unavailable due to maintenance events, used in the fleet utilisation analysis alongside the `utilization_rate` from `truck_utilization_metrics`.

**Total Maintenance Cost** sums `total_cost` from `maintenance_records` formatted as Currency. Each maintenance record already contains the total cost (labour plus parts), so a simple sum is the correct aggregation.

**Total Load Delivered** counts rows in the `loads` table. Since each row is one load, `COUNTROWS` is correct. The Decimal Number format is unusual for a count — formatting as Whole Number would be cleaner, but the value displayed (85K) is unaffected.

**Revenue % by customer type** uses `ALL(customers[customer_type])` to remove the filter on customer type before calculating the denominator. This means the denominator is always the total revenue regardless of which customer type is selected, giving a genuine percentage share rather than 100% for each type individually.

**Profit Margin%** divides `Route Profit` (a calculated column on `routes`) by `Total Revenue`. This is the gross margin at the route level. It is formatted as Percentage and used as the headline margin KPI on the Overview page.

**Profit per Driver** divides the same `Route Profit` by the distinct count of driver IDs. This gives the average profit contribution per driver across the entire fleet — a useful benchmark for workforce productivity.

**Late Deliveries** uses `CALCULATE` with two explicit filters: `event_type = "Delivery"` excludes pickup events (which have different on-time rates), and `on_time_flag = FALSE` selects only the late ones. Both filters together ensure this measure counts late delivery scans only, not any other event type.

**Active Drivers** counts distinct `driver_id` values across the entire `drivers` table. Note that this gives the total driver headcount in the table — it does not filter for `employment_status = Active`. If the table contains terminated drivers, this count would include them. Adding a filter for active employment status would make this measure more precise.

**On-time-delivery %** uses `FILTER` to count only rows where `on_time_flag = TRUE`, then divides by the total row count of `delivery_events`. This includes both pickup and delivery events in the denominator — which is why the result (55.67%) reflects a blended pickup-and-delivery rate. A delivery-only version would filter `event_type = "Delivery"` in both the numerator and denominator.

**Total Customers** counts distinct `customer_id` values in the `customers` table, returning 200 — the total number of unique customer accounts in the dataset.

---

## 📈 Key Metrics Summary

### Overview

| Metric | Value |
|---|---|
| Total Revenue | **$298.6M** |
| Total Profit | **$197.3M** |
| Total Miles Driven | **122M** |
| Average MPG | **6.50** |
| Profit Margin | **66.07%** |
| Fleet Utilisation Rate | **83%** |
| Average Revenue per Load | **$3,500** |
| Total Fuel Cost | **$95.6M** |
| Total Maintenance Cost | **$5.7M** |

### Drivers & Route Performance

| Metric | Value |
|---|---|
| On-Time Delivery Rate | **55.67%** |
| Late Deliveries | **47,308** |
| Active Drivers | **150** |
| Profit per Driver | **$1.32M** |
| Top Lane by Profit | **NC → OR ($3.9M)** |
| Dedicated Booking Share | **49.57%** |

### Maintenance & Safety

| Metric | Value |
|---|---|
| Total Damage Cost | **$1.60M** |
| Preventable Incident Rate | **37.65%** |
| Total Downtime Hours | **72,230** |
| Total Maintenance Cost | **$5.7M** |
| Top Incident Type | **DOT Violation (39)** |
| Top Terminal by Incidents | **Indianapolis (14)** |

### Customers Analysis

| Metric | Value |
|---|---|
| Total Customers | **200** |
| Total Loads Delivered | **85,410** |
| Top Customer by Revenue | **First Group ($10.4M)** |
| Average On-Time Rate | **55.67%** |
| Monthly Profit Range | **$9.9M – $11.7M** |

---

## 💡 Key Insights

**1. On-time delivery is the most critical operational failure.**
Only 55.67% of 85,410 loads were delivered on time, meaning 47,308 deliveries arrived late. The industry standard for on-time delivery exceeds 90%. This gap represents a systemic service quality problem that puts customer contract renewals at risk across all 200 accounts.

**2. The lateness is not a driver capacity problem.**
When pickups succeed at a materially higher rate than deliveries, delays are accumulating during the trip — most likely from extended detention at customer receiving facilities. Adding drivers would not solve this. Negotiating dwell time with high-detention customers would.

**3. Fleet utilisation at 83% leaves meaningful headroom.**
Approximately 17% of truck capacity sits idle. Before investing in additional equipment, optimising dispatch scheduling and reducing empty miles between loads would improve asset productivity without capital expenditure.

**4. The NC → OR lane is the single most profitable route at $3.9M.**
The top three lanes each generate over $3.5M. The bottom three generate under $1.5M. A 2.5x profit spread between best and worst lanes indicates significant pricing variation — underpriced lanes are being cross-subsidised by premium routes.

**5. Over one in three safety incidents was preventable.**
37.65% of incidents resulting in damage or claims could have been avoided. At $1.60M in total damage cost over three years, a driver safety coaching programme targeting DOT violations and moving violations would generate measurable ROI.

**6. DOT violations are the most frequent incident type at 39 cases.**
DOT violations outnumber accidents (35) and equipment damage (35), suggesting a compliance culture issue addressable through operational process changes — hours-of-service monitoring, pre-trip inspection protocols — rather than capital spending.

**7. Indianapolis and Las Vegas terminals carry the highest incident load.**
Both recorded 14 incidents each, significantly more than lower-incident terminals at 8. Terminal-level concentration suggests local management practices or route types at those locations differ from better-performing terminals.

**8. Preventive maintenance is the largest cost category at $963.6K — and that is positive.**
Proactive servicing is more efficient than reactive repairs. However, with brake and engine maintenance each approaching $900K, the drivetrain burden suggests fleet ageing that may justify an accelerated replacement cycle for high-mileage assets.

**9. First Group is the anchor customer and a concentration risk.**
At $10.4M from 3,001 loads, First Group is 30% larger than the next customer. If this account reduces or cancels its contract, the remaining 199 customers cannot immediately absorb the volume gap.

**10. The booking mix is nearly equal across three channels.**
Contract (37.64%), Spot (31.55%), and Dedicated (30.81%) revenue are well balanced, which reduces dependency risk. However, Dedicated bookings typically carry lower per-load rates in exchange for volume guarantees — monitoring whether Dedicated rates still reflect market conditions is important as freight pricing evolves.

**11. Monthly profit shows a predictable seasonal pattern.**
Profit ranges from $9.9M in February to $11.7M in January — a $1.8M swing. February is structurally weaker in US freight due to post-holiday volume drops, weather disruptions, and fewer calendar days. Recognising this allows better cash flow planning and staffing alignment.

**12. A 0.25 MPG improvement across the fleet is worth roughly $1.5M annually.**
At 6.50 MPG across 122 million miles and $95.6M in fuel cost, reducing idle time through driver coaching is one of the highest-return operational interventions available without any capital investment.

---

## 📢 Business Recommendations

**1. Investigate detention at customer facilities before adding capacity.**
Audit dwell times by customer location, identify the facilities causing the longest delays, and incorporate detention accountability clauses into contract renewals. Resolving detention will improve on-time rates without headcount increases.

**2. Launch a targeted safety coaching programme at Indianapolis and Las Vegas.**
These two terminals account for a disproportionate share of incidents. Route-specific safety briefings, dashcam review sessions, and hours-of-service monitoring would reduce the preventable rate and its associated damage costs.

**3. Reprice underperforming lanes based on cost-per-mile analysis.**
The gap between the most and least profitable lanes is too large to ignore. Lanes should be reviewed against their actual cost structure — fuel, driver pay, and maintenance allocation — and either repriced, renegotiated, or removed from active load acceptance.

**4. Develop a key account service programme for the top 10 customers.**
Every top-10 customer is receiving on-time delivery at approximately 54–57%. Dedicated account reviews, SLA transparency, and priority dispatch for highest-value accounts would meaningfully reduce contract renewal risk.

**5. Build a fleet replacement schedule for high-maintenance assets.**
Identifying the trucks with the highest maintenance cost per mile and scheduling them for planned replacement would reduce unplanned downtime hours and improve the utilisation rate beyond the current 83%.

**6. Review Dedicated booking rates against current market conditions.**
At 49.57% of all loads, Dedicated represents the largest booking channel. Ensuring Dedicated rates reflect current fuel and labour costs — rather than rates locked in at contract signing — protects margin on nearly half the business.

---

## 🔄 Project Workflow

```
14 Raw Source Tables (CSV / Excel)
            │
            ▼
  Data Cleaning in Power Query
  ├── Remove duplicates
  ├── Fix data types
  ├── Standardise text columns
  ├── Handle missing values
  └── Build central Date table
            │
            ▼
  Data Modelling (Star Schema)
  ├── Define relationships (1-to-many)
  ├── Set filter directions (single)
  └── Connect Date table to all facts
            │
            ▼
  DAX Measures
  ├── Revenue, Profit, Margin %
  ├── On-Time Delivery %
  ├── Late Deliveries count
  ├── Fleet Utilisation Rate
  ├── Preventable Incident Rate
  └── Cost per Mile
            │
            ▼
  4-Page Interactive Dashboard
  ├── Page 1: Overview
  ├── Page 2: Drivers & Route Performance
  ├── Page 3: Maintenance & Safety
  └── Page 4: Customers Analysis
            │
            ▼
  Key Insights & Business Recommendations
```

---

## 📁 Folder Structure

```
Logistics-Operations-Dashboard/
│
├── 📂 Data/
│   ├── customers.csv
│   ├── drivers.csv
│   ├── trucks.csv
│   ├── trailers.csv
│   ├── routes.csv
│   ├── facilities.csv
│   ├── loads.csv
│   ├── trips.csv
│   ├── fuel_purchases.csv
│   ├── maintenance_records.csv
│   ├── delivery_events.csv
│   ├── safety_incidents.csv
│   ├── driver_monthly_metrics.csv
│   └── truck_utilization_metrics.csv
│
├── 📂 Dashboard/
│   └── Logistics_Operations_Dashboard.pbix
│
├── 📂 SQL/
│   └── validation_queries.sql
│
├── 📂 Images/
│   ├── LOGIS.png                  ← Overview page
│   ├── LOGIS2.png                 ← Drivers & Route Performance
│   ├── LOGIS3.png                 ← Maintenance & Safety
│   ├── LOGIS1.png                 ← Customers Analysis
│   ├── model_view.png             ← Data model relationship diagram
│   ├── dax_avg_mpg.png            ← AVG MPG measure
│   ├── dax_total_miles.png        ← Total Miles Driven measure
│   ├── dax_total_incidents.png    ← Total Incidents measure
│   ├── dax_fuel_cost_per_lane.png ← Fuel Cost per Lane measure
│   ├── dax_downtime.png           ← Total Downtime Hour measure
│   ├── dax_maintenance_cost.png   ← Total Maintenance Cost measure
│   ├── dax_total_loads.png        ← Total Load Delivered measure
│   ├── dax_revenue_pct.png        ← Revenue % by Customer Type measure
│   ├── dax_profit_margin.png      ← Profit Margin % measure
│   ├── dax_profit_per_driver.png  ← Profit per Driver measure
│   ├── dax_late_deliveries.png    ← Late Deliveries measure
│   ├── dax_active_drivers.png     ← Active Drivers measure
│   ├── dax_otd.png                ← On-time-delivery % measure
│   └── dax_total_customers.png    ← Total Customers measure
│
└── README.md
```

---

## 🧠 Skills Demonstrated

| Skill | Evidence |
|---|---|
| **Data Modelling** | 14-table star schema with one-to-many relationships |
| **Power Query** | Cleaning, type fixing, deduplication, and Date table creation |
| **DAX Measures** | Revenue, margin, OTD%, cost per mile, preventable incident rate |
| **Time Intelligence** | Central Date table with year, quarter, month slicers |
| **Dashboard Design** | 4-page interactive report with consistent green/white design system |
| **KPI Selection** | Headline metrics chosen for operational and executive relevance |
| **Multi-table Modelling** | 14 tables connected in a clean star schema |
| **Data Storytelling** | Findings framed as business problems with actionable implications |
| **Business Analysis** | Recommendations grounded in specific data patterns |
| **SQL Validation** | Cross-table joins used to verify model accuracy pre-visualisation |

---

## 📝 Results Summary

This project transforms 14 connected logistics tables — covering 85,410 loads, 150 drivers, 200 customers, and 122 million miles of operations — into a four-page interactive Power BI dashboard that gives logistics managers complete visibility into their business. The analysis uncovered a 55.67% on-time delivery rate against an industry standard above 90%, identified the NC → OR lane as the most profitable at $3.9M, found that 37.65% of safety incidents were preventable, and revealed that Indianapolis and Las Vegas terminals carry disproportionate incident risk. Total revenue of $298.6M is strong, but the service quality picture demands operational attention before customer contracts come up for renewal. The dashboard equips decision-makers to address these issues with evidence rather than instinct.

---

## 🚀 Future Improvements

- **Predictive on-time delivery model** — identify at-risk loads before dispatch using historical trip patterns, enabling proactive rerouting or customer communication
- **Driver drill-through detail page** — click any driver name to open a full performance profile showing trip history, fuel efficiency trend, incident log, and month-over-month metrics
- **Lane profitability map** — US route map with lines coloured by profit per mile, making underperforming corridors immediately visible
- **Maintenance cost forecasting** — project next-quarter maintenance spend by truck based on historical service intervals and current odometer readings
- **Real-time data refresh** — connect the model to SQL Server or Azure for scheduled or real-time refresh, replacing the static CSV source files
- **Customer churn risk indicator** — flag accounts whose on-time delivery rate has declined over three consecutive months as a leading indicator of contract risk

---

## ✅ Conclusion

This logistics operations dashboard demonstrates what becomes possible when operational data is treated as a strategic asset rather than a by-product of daily activity. By connecting 14 tables, building a clean star schema, and developing targeted DAX measures, the project delivers a tool that gives logistics leadership visibility into every dimension of the operation — from individual driver performance to route-level profitability to safety incident root causes. The central finding — that more than 44% of deliveries arrive late despite strong revenue performance — is the kind of insight that only surfaces when operational data is connected and examined as a whole. This is the business value that data analytics delivers.

---

## 👤 Author

**Eke Deborah** — Data Analyst | Power BI · SQL · Python · Excel

- 🔗 [LinkedIn](https://www.linkedin.com/in/your-linkedin)
- 📧 your.email@gmail.com
- 🐙 [GitHub](https://github.com/your-username)

---

*Built as part of a data analytics portfolio. Dataset covers a simulated US trucking operation spanning 2022–2024.*
