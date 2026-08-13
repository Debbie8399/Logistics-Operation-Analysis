# 🚛 Logistics Operations Power BI Dashboard

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
- [Future Improvements](#future-improvements)
- [Conclusion](#conclusion)

---

## 📌 Project Overview
This project delivers a fully interactive **4-page Power BI dashboard** analysing the end-to-end operations of a US-based trucking and logistics company.  
The analysis covers **85,410 loads, 150 active drivers, 200 customers, and 122 million miles** of freight movement from **2022 to 2024**.

**Business Problem**: Data was spread across 14 disconnected systems. Managers couldn’t see profitable routes, underperforming drivers, or safety risks.  
**Solution**: Unified all data into one Power BI model to drive data-based decisions.

**Total Revenue**: $298.6M  
**On-Time Delivery Rate**: 55.67% ← *Key issue identified*

---

## 📊 Dashboard Pages

### Page 1 — Overview
Executive KPIs, Top 10 Customers, Revenue Split, Incident Trends, Fleet Utilisation
![Overview Dashboard](images/LOGIS.png)

### Page 2 — Drivers & Route Performance  
OTD Rate, Late Deliveries, Profit per Driver, Route Profitability
![Drivers & Route Performance](images/LOGIS2.png)

### Page 3 — Maintenance & Safety
Damage Cost, Incident Rate, Downtime, Maintenance by Type
![Maintenance & Safety](images/LOGIS3.png)

### Page 4 — Customers Analysis
Customer Revenue, Load Volume, Late Deliveries by Customer
![Customers Analysis](images/LOGIS1.png)

---

## 🗂 Dataset Information
| Attribute | Details |
| --- | --- |
| Total Tables | 14 |
| Total Loads | 85,410 |
| Total Customers | 200 |
| Active Drivers | 150 |
| Total Miles Driven | 122,159,201 |
| Period Covered | Jan 2022 – Dec 2024 |

---

## 🛠 Tools & Technologies
| Tool | Purpose |
| --- | --- |
| Power BI Desktop | Dashboard & Data Modelling |
| Power Query | Data Cleaning & Transformation |
| DAX | KPIs and Measures |
| SQL | Data Validation |
| Excel / CSV | Source Data |

---

## 🧹 Data Cleaning & Preparation
- Removed duplicates across 14 tables
- Fixed data types: Date, Decimal, Text
- Standardised text: city names, booking types
- Created central Date table for time intelligence
- Built star schema with single-direction relationships

---

## 🔗 Data Model & Relationships
Star schema with `trips` as the central fact table.  
Connected to customers, drivers, trucks, routes, loads, fuel, maintenance, and incidents.

![Data Model](images/model_view.png)

---

## 📐 Key DAX Measures
- **Total Revenue**: $298.6M
- **Profit Margin %**: 66.07%
- **On-time Delivery %**: 55.67%
- **Late Deliveries**: 47,308
- **AVG MPG**: 6.50
- **Total Miles Driven**: 122M

*Full measure list and screenshots available in `/images/` folder*

---

## 📈 Key Metrics Summary

**Overview**
| Metric | Value |
| --- | --- |
| Total Revenue | $298.6M |
| Total Profit | $197.3M |
| Fleet Utilisation | 83% |
| Avg Revenue per Load | $3,500 |

**Drivers & Routes**
| Metric | Value |
| --- | --- |
| On-Time Delivery Rate | 55.67% |
| Top Lane by Profit | NC → OR ($3.9M) |
| Profit per Driver | $1.32M |

---

## 💡 Key Insights
1. **OTD Crisis**: Only 55.67% on-time. Industry standard >90%
2. **Detention Issue**: Delays happen at customer facilities, not from driver shortage
3. **Lane Profit Gap**: Top lane $3.9M vs bottom lane <$1.5M
4. **Safety**: 37.65% of incidents were preventable. $1.6M damage cost
5. **Fuel Opportunity**: 0.25 MPG improvement = ~$1.5M savings

---

## 📢 Business Recommendations
1. Audit customer dwell time and add detention clauses
2. Safety coaching for Indianapolis and Las Vegas terminals  
3. Reprice underperforming lanes
4. Key Account program for Top 10 customers
5. Fleet replacement schedule for high-maintenance trucks

---

## 📁 Folder Structure
