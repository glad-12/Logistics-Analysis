
# Logistics Analytics Dashboard (2022–2024)

**Data Analytics Capstone | Portfolio Project**
**Author:** Ulegu Gladys

A four-page Power BI dashboard built from **14 logistics datasets**. It tracks revenue, lane profitability, driver productivity, fuel efficiency, customer claims and fleet performance across 2022–2024, turning raw trucking data into decisions that protect margin and cut operating waste.

---

##  Table of Contents

1. [Project Overview](#-project-overview)
2. [Business Problem](#-business-problem)
3. [Objectives and Business Questions](#-objectives-and-business-questions)
4. [Tools and Methodology](#-tools-and-methodology)
5. [Data Preparation](#-data-preparation)
6. [Key Findings](#-key-findings)
7. [Recommendations](#-recommendations)
8. [Dashboard Preview](#-dashboard-preview)
9. [Conclusion](#-conclusion)
10. [Skills Demonstrated](#-skills-demonstrated)

---

##  Project Overview

This capstone analyses the operations of a US trucking and freight company over three years. The company's data was spread across **14 separate CSV files** covering trucks, trailers, drivers, customers, facilities, routes, trips, loads, fuel purchases, maintenance, safety incidents, delivery events, driver monthly metrics and truck utilization.

I cleaned, modelled and connected these files into one data model, then built a four-page interactive dashboard:

| Page | Focus |
|------|-------|
| 1 | Revenue and Lane Profitability |
| 2 | Driver Productivity and Fuel Efficiency |
| 3 | Customer Revenue and Claims Overview |
| 4 | Fleet Efficiency Overview |

---

## Business Problem

The company moves **85,000+ loads** and **122 million miles** of freight, generating about **262.5M** in load revenue. Yet the business has no single view of how well that activity performs.

1. **Flat revenue:** 87.85M (2022) → 86.96M (2023) → 87.72M (2024). The same freight is moved year after year with no real growth.
2. **Unclear lane profitability:** Revenue per mile is about 2.15 across all booking types, so leadership cannot easily tell which lanes, cities and booking types deserve more capacity.
3. **Weak delivery reliability:** On-time delivery sits at roughly **45%** and barely moves month to month, putting customer relationships and contract renewals at risk.
4. **Unexplained fuel losses:** A fuel gap of about **22.67%** exists between fuel bought and fuel used. This could mean waste, data capture errors or leakage.
5. **Rising claims and uneven driver risk:** Total claims reached **2.65M**, with a small group of drivers responsible for a large share. Cargo damage alone is over 60% of claim cost.
6. **Idle and underused assets:** Truck downtime exceeds **54,000 hours**, fuel economy is stuck at about **6.45 MPG**, and idle time is 0.28 per trip.

Because the data lived in 14 disconnected files, none of these problems could be seen, measured or acted on together. This project solves that.

---

## Objectives and Business Questions

**Objective:** Build one reliable, interactive reporting solution that helps management grow revenue, improve delivery performance, control fuel and claims costs, and use the fleet more efficiently.

**Business questions answered:**

- Which booking types and destination cities earn the most revenue per mile?
- Is load revenue growing year over year?
- How productive is each driver, and how reliable are deliveries month to month?
- How much fuel is bought versus used, and what is the fuel surcharge impact?
- Which customers, customer types and account statuses drive revenue?
- Which incident types and drivers cause the most claims, and is cargo or vehicle damage costing more?
- Which truck makes and facilities contribute most to revenue, downtime and capacity?

---

## Tools and Methodology

| Stage | Tool | Purpose |
|-------|------|---------|
| 1 | Data cleaning | Fix data types, remove duplicates and nulls, standardise text and IDs |
| 2 | Power Query | Import the 14 CSVs, transform, merge and shape the tables |
| 3 | Power BI | Build the data model, visuals, slicers and page navigation |
| 4 | DAX | Create KPIs such as revenue per mile, fuel gap % and on-time rate |

**Workflow:** Import and profile the data → clean and transform it → model it as a star schema → write DAX measures → design the dashboard pages → draw insights and recommendations from the visuals.

---

##  Data Preparation

### Data Cleaning
- Checked each of the 14 files for duplicates, blank values and inconsistent spellings (e.g. city names and booking types).
- Corrected data types for dates, currency, miles and gallons.
- Standardised IDs (driver, truck and customer) so tables could be joined reliably.
- Validated numbers, e.g. confirming that trips, loads and miles reconciled across tables.

### Power Query
- Loaded all 14 CSV files and promoted headers.
- Removed unused columns and filtered out invalid rows.
- Merged and shaped tables to bring in fields such as booking type, destination city, truck make and facility type.
- Created a Date table to support year, month and quarter analysis.

### Data Modelling
- Arranged the data as a **star schema**: fact tables (trips, loads, fuel purchases, maintenance, safety incidents, delivery events) linked to dimension tables (drivers, trucks, customers, facilities, routes, date).
- Used one-to-many relationships with single-direction filtering for clean, fast calculations.

### DAX Measures (examples)

```dax
Total load Revenue= SUM(Loads[load_revenue])

Total Miles = SUM(Trips[actual_distance_miles])

Revenue Per Mile = DIVIDE([Total Load Revenue], [Total Miles])

Avg Revenue Per Load =
    DIVIDE([Total Load Revenue], DISTINCTCOUNT(Loads[load_id]))

Fuel Gap % = DIVIDE([Fuel Used] - [Fuel Bought], [Fuel Used])

On Time Delivery Rate =
    DIVIDE(
        CALCULATE(
            COUNTROWS(DeliveryEvents),
            DeliveryEvents[on_time_flag] = TRUE()
        ),
        COUNTROWS(DeliveryEvents)
    )

Total Claims = SUM(SafetyIncidents[claim_amount])

Revenue Per Customer =
    DIVIDE([Annual Customer Revenue], DISTINCTCOUNT(Customers[customer_id]))
```

---

##  Key Findings

### Page 1: Revenue and Lane Profitability
- Total load revenue is **262.53M** from 85K loads and 122M miles, giving **2.15 revenue per mile** and about 3.07K per load.
- **Dedicated** bookings lead with 130.24M (49.61%) of revenue and the best margin at 2.2 per mile, versus 2.1 for Spot and Contract.
- Spot (~66M) and Contract (~66M) each bring in roughly a quarter of revenue.
- Revenue is flat: 87.85M (2022), 86.96M (2023), 87.72M (2024).
- **Philadelphia, Portland and Charlotte** lead the top destination cities by revenue per mile.

### Page 2: Driver Productivity and Fuel Efficiency
- Drivers generated 257.26M in revenue, averaging **683 trips per driver**. The busiest drivers (e.g. DRV00019) complete about 749 trips.
- On-time delivery is stuck near **44.61%**, moving between about 43.8% and 45.6% all year with no seasonal improvement.
- A **22.67% fuel gap** exists between fuel bought (18.95M) and fuel used (24.5M), which needs reconciling.
- Fuel surcharge averages 350.97 per load and is steady at about 10M a year.

### Page 3: Customer Revenue and Claims
- 200 customers generate **538M** in annual customer revenue, about 2.69M per customer.
- Active accounts bring in 439M against **98M from inactive accounts**, a sizeable pool to win back.
- Revenue is spread fairly evenly across Contract (207M, 38.5%), Dedicated (169M, 31.5%) and Spot (161M, 30%).
- Total claims are **2.65M**: 1.02M in 2022, 0.79M in 2023 and 0.84M in 2024.
- **Cargo damage** costs 1.6M (60.44%) versus 1.05M for vehicle damage.
- Equipment damage (0.74M) and DOT violations (0.58M) are the costliest incident types. The top claim driver (DRV00058) accounts for about 117.6K.

### Page 4: Fleet Efficiency
- The network has **3,929 dock doors**, led by Cross-Dock (1,452) and Distribution Centers (1,070).
- Average fuel economy is **6.45 MPG**, flat across all 12 months. Idle time is 0.28 per trip.
- Miles are steady at about 40–41M a year across all three years.
- **Volvo** trucks earn the most revenue (53.17M) but also log the most downtime (12,282 hours). Total downtime is **54,812 hours**.

---

## Recommendations

1. **Prioritise Dedicated bookings.** They earn half of revenue at the best rate per mile. Offer incentives to convert Spot and Contract customers.
2. **Invest in the top lanes.** Allocate more trucks and drivers to Philadelphia, Portland and Charlotte, which pay the most per mile.
3. **Break the revenue plateau.** Set a growth target, re-price low-margin lanes and win back inactive accounts worth 98M.
4. **Fix on-time delivery.** Investigate delay causes (loading time, routing, dock congestion) and set a target well above 45%. Review driver scheduling and route planning.
5. **Reconcile the fuel gap.** Audit fuel purchase records against trip fuel usage, introduce fuel-card controls and flag unusual purchases.
6. **Reduce cargo damage claims.** Improve loading, securing and handling procedures, since cargo damage drives over 60% of claim cost.
7. **Coach high-claim drivers.** Provide targeted safety training for drivers with the largest claim totals and recognise safe, high-productivity drivers.
8. **Cut downtime and idling.** Introduce preventive maintenance schedules, review Volvo maintenance costs and set idle-time targets to lift MPG.

---

## Dashboard Preview

Each page includes year slicers (2022, 2023, 2024), page navigation buttons and KPI cards.

### Page 1: Revenue and Lane Profitability

<img width="973" height="583" alt="image" src="https://github.com/user-attachments/assets/af69d5e2-b87c-4525-963f-a1dc0ca951b0" />

### Page 2: Driver Productivity and Fuel Efficiency
<img width="998" height="576" alt="image" src="https://github.com/user-attachments/assets/418cc02b-b75d-4155-8984-cf938060740a" />


### Page 3: Customer Revenue and Claims

<img width="957" height="582" alt="image" src="https://github.com/user-attachments/assets/96666981-e839-4cf1-b132-7041846db598" />

### Page 4: Fleet Efficiency

<img width="966" height="579" alt="image" src="https://github.com/user-attachments/assets/6652832e-d763-4064-99f1-0f35be024cd5" />


---

## Conclusion

Operations are steady but not improving. Revenue is flat, deliveries are on time less than half the time, fuel does not reconcile, and cargo claims and downtime keep costs high. The biggest opportunities are growing Dedicated and top-lane business, fixing delivery reliability, closing the fuel gap and reducing cargo damage.

By bringing 14 scattered datasets into one interactive Power BI dashboard, I created a single source of truth that lets management monitor performance, find problems early and act with confidence.

---

## Skills Demonstrated

`Data Cleaning` · `Power Query` · `Data Modelling (Star Schema)` · `DAX` · `Dashboard Design` · `Business Storytelling` · `Recommendation Writing`


---

## Contact

**Ulegu Gladys**
Data Analytics | Business Analysis
https://www.linkedin.com/in/gladys-ulegu-a934a7353
glademma234@gmail.com

