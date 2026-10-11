# End-to-End Logistics Performance Analytics

An end-to-end data analytics project using SQL, Excel, Power Query, and Power BI to examine logistics financial performance, fleet efficiency, driver safety, and delivery operations.

## Project Overview

This project analyses logistics operations using SQL and Power BI, covering revenue and route profitability, driver performance and safety, fleet utilisation, fuel consumption, maintenance costs, and delivery operations.

The analysis combines operational and financial metrics to examine performance across different areas of the logistics business. Four Power BI dashboard pages were developed to present key performance indicators, compare operational patterns, and support further investigation of business performance.

## Business Problem

Logistics businesses need visibility into revenue generation, route profitability, fleet efficiency, driver performance, maintenance expenditure, and delivery operations.

This project examines these areas to identify performance patterns, highlight areas that may require further investigation, and present operational data in a structured dashboard format.

## Project Objectives

- Analyse revenue, profit, and route profitability.
- Examine revenue contributions from customers and routes.
- Evaluate driver performance, delivery timeliness, and safety incidents.
- Investigate fleet utilisation, mileage, fuel costs, and maintenance expenditure.
- Analyse delivery operations, trip duration, and facility detention time.
- Present key performance indicators through Power BI dashboards.

## Tools and Technologies

- **SQL** — Used to select relevant fields, clean text values, rename columns, transform categorical values, and prepare data for analysis.
- **Microsoft Excel** — Used to work with the structured source data tables.
- **Power Query** — Used to inspect the data, check for potential duplicates, and review data distribution.
- **Power BI** — Used to build four interactive dashboard pages, create DAX measures, and visualise financial and operational performance metrics.

## Dataset Overview

The project uses 14 data tables covering different aspects of logistics operations.

| Table | Description |
|---|---|
| `customers` | Customer information |
| `loads` | Load and shipment records |
| `trips` | Trip-level operational records |
| `routes` | Route information |
| `drivers` | Driver details |
| `driver_monthly_metrics` | Monthly driver performance metrics |
| `trucks` | Truck and fleet information |
| `trailers` | Trailer information |
| `truck_utilization_metrics` | Truck utilisation metrics |
| `fuel_purchases` | Fuel purchase records |
| `maintenance_records` | Maintenance activities and costs |
| `safety_incidents` | Driver or fleet safety incidents |
| `delivery_events` | Delivery event records |
| `facilities` | Facility information |

## Data Preparation and SQL

I prepared the logistics data for analysis using SQL, working with tables covering customers, loads, trips, routes, drivers, fleet operations, fuel purchases, maintenance, safety incidents, and delivery events. My preparation work focused on selecting relevant fields, improving field readability, cleaning text values, and preparing categorical fields for reporting.

### SQL Transformations

SQL was used to prepare the source tables for analysis through the following operations:

- **Column selection:** Selected relevant fields from the source tables.
- **Column aliases:** Renamed selected fields to improve readability.
- **Text cleaning:** Used `TRIM()` to remove unwanted leading and trailing whitespace from text values.
- **Categorical transformations:** Used `CASE` statements to convert state abbreviations into readable state names.
- **Text concatenation:** Used `CONCAT()` to combine driver first and last names.
- **Flag transformations:** Converted numeric indicator fields into readable Boolean labels.
- **Field preparation:** Prepared selected columns for subsequent analysis and reporting.

### Data Inspection

I used Power Query to inspect the datasets, check for potential duplicate records, and review data distribution. This step helped me examine the source data before proceeding with the analysis. I did not use Power Query for substantial data transformations or table combinations.

### Power BI

I used Power BI to build four dashboard pages, create DAX measures, and analyse financial and operational performance across the logistics business.

The dashboards cover:

- **Customer, Revenue and Route Profitability:** Revenue, profit, profit margin, and customer revenue potential.
- **Driver Performance and Safety:** Driver revenue, completed trips, on-time delivery rate, fuel efficiency, and safety incidents.
- **Fleet, Fuel and Maintenance:** Fleet utilisation, fuel costs, mileage, maintenance costs, and downtime.
- **Operations and Delivery:** Load volume, trip duration, delivery timeliness, detention time, and revenue per mile.

I used KPI cards and visualisations to present performance metrics and make it easier to compare results across the different areas of the business.

## DAX Measures and Power BI Calculations

I created DAX measures in Power BI to calculate key financial, operational, fleet, driver, and safety performance metrics. These calculations supported the KPI cards and visualisations across the four dashboard page

### Selected DAX Measures

**1. Total Revenue**

Calculates revenue from the loads dataset.

```dax
Total Revenue = SUM(Loads[revenue])
```

**2. Total Miles**

Calculates the total actual distance recorded across trips.

```dax
Total Miles = SUM(Trips[actual_distance_miles])
```

**3. Revenue per Mile**

Measures revenue relative to the total recorded trip distance.

```dax
Revenue per Mile =
DIVIDE(
    [Total Revenue],
    [Total Miles]
)
```

**4. Total Profit**

Calculates revenue less recorded fuel and maintenance costs.

```dax
Total Profit =
    [Total Revenue]
    - [Total Fuel Cost]
    - [Total Maintenance Cost]
```

This measure reflects the costs included in the calculation and should not be interpreted as definitive net profit.

**5. Profit Margin**

Calculates the proportion of revenue represented by the profit measure.

```dax
Profit Margin =
DIVIDE(
    [Total Profit],
    [Total Revenue]
)
```

**6. On-Time Delivery Rate**

Calculates the proportion of delivery-event records marked as on time.

```dax
On-Time Delivery Rate =
DIVIDE(
    CALCULATE(
        COUNTROWS(Delivery_Events),
        Delivery_Events[on_time_flag] = TRUE()
    ),
    COUNTROWS(Delivery_Events)
)
```

This measure reports the percentage of delivery-event records marked as on time, based on the records included in the analysis.

**7. Average Utilisation Rate**

Calculates the average recorded fleet utilisation rate.

```dax
Average Utilization Rate =
AVERAGE('Truck Utilization Metrics'[utilization_rate])
```

**8. Total Maintenance Cost**

Calculates the sum of recorded maintenance costs.

```dax
Total Maintenance Cost =
SUM(Maintenance_Records[total_cost])
```

### Additional Calculations

The project also includes measures for completed trips, average trip duration, average detention time, fuel expenditure, fuel consumption, downtime, safety incidents, preventable incidents, customer revenue potential, driver counts, active drivers, and driver revenue.

A calculated column named `Route Label` combines origin and destination information to create readable route labels for analysis.

Together, these calculations support the financial, operational, fleet, driver, delivery, and safety metrics presented in the dashboards.
## Dashboard Analysis

### 1. Customer, Revenue & Route Profitability
![Customer, Revenue and Route Profitability Dashboard](assets/logistics-revenue-route.%20jpg.png)

I developed this dashboard to analyse revenue, profitability, customer contribution, and route performance across the logistics operation.

**Key performance indicators**
- Total Revenue: $262.53M
- Profit: $161.20M
- Profit Margin: 61.40%
- Average Revenue per Load: $3.07K
- Revenue per Mile: $2.15
- Total Customers: 200
- Customer Revenue Potential: $538M

**Analysis areas**
- Revenue and cost breakdown
- Revenue by customer
- Revenue by destination state
- Revenue by customer type
- Top routes by revenue
- Top routes by profit

### 2. Driver Performance & Safety
![Drivers Performance and Safety Dashboard](assets/logistics-driver-safety.%20jpg.png)

I developed this dashboard to analyse driver performance, delivery timeliness, fuel efficiency, and safety incidents across the logistics operation.

**Key performance indicators**
- Active Drivers: 124
- Driver Revenue: $257.26M
- On-Time Delivery Rate: 55.67%
- Completed Trips: 85K
- Average MPG: 6.45
- Total Safety Incidents: 170
- Preventable Incidents: 64

**Analysis areas**
- Driver mileage and revenue
- On-time delivery performance
- Revenue per mile
- Safety incident counts by driver
- Comparison of driver performance metrics

### 3. Fleet, Fuel & Maintenance
![Fleet, Fuel and Maintenance Dashboard](assets/logistics-fleet-maintenance.%20jpg.png)

I developed this dashboard to analyse fleet utilisation, fuel efficiency, fuel expenditure, maintenance costs, and vehicle downtime.

**Key performance indicators**
- Total Fleet: 120
- Total Fuel Cost: $95.59M
- Total Downtime Hours: 72.23K
- Total Maintenance Cost: $5.73M
- Average Utilisation Rate: 83.04%
- Average MPG: 6.45
- Total Miles: 122M

**Analysis areas**
- Monthly fleet utilisation
- Top trucks by mileage
- Fuel efficiency by truck
- Maintenance cost by truck
- Fleet status distribution
- Monthly fuel costs

### 4. Operations & Delivery Performance
![Operations and Delivery Performance Dashboard](assets/logistics-operations-delivery.%20jpg.png)

I developed this dashboard to analyse load volumes, revenue trends, trip duration, fuel usage, and delivery delays across routes and facilities.

**Key performance indicators**
- Total Loads: 85K
- Total Revenue: $262.53M
- On-Time Delivery Rate: 55.67%
- Completed Trips: 85K
- Average Trip Duration: 25.01 hours
- Average Detention: 91.54 minutes
- Revenue per Mile: $2.15

**Analysis areas**
- Monthly loads and revenue
- Fuel gallons used
- Facilities with the highest detention time
- Revenue by route
- Detention minutes by facility city
- Average trip duration by route
## Key Findings

The Power BI dashboards bring together financial, delivery, fleet, and driver safety metrics to highlight areas of performance and potential operational improvement.

### 1. Revenue and Profitability

The analysis reports **$262.53M in total revenue**, **$161.20M in calculated profit**, and a **61.40% profit margin**.

These metrics provide a view of revenue generation and profitability based on the costs included in the model. The profit measure deducts recorded fuel and maintenance costs from revenue, so the result should be interpreted within that scope.

### 2. Delivery Performance

The reported on-time delivery rate is **55.67%**, highlighting delivery timeliness as an area that warrants further investigation.

Comparing delivery events across routes and facilities can help identify where delays occur and where operational improvements may be needed.

### 3. Fleet Utilisation and Operating Costs

The analysis reports an average fleet utilisation rate of **83.04%**, alongside **$95.59M in fuel costs**, **$5.73M in maintenance costs**, and **72.23K downtime hours**.

Viewed together, these metrics help assess fleet usage alongside fuel expenditure, maintenance spending, and vehicle downtime. Further analysis could investigate how these factors relate to fleet efficiency and operating costs.

### 4. Driver Safety

The safety dashboard records **170 safety incidents**, of which **64 are classified as preventable**.

These figures establish a basis for examining incident patterns and identifying drivers, routes, or operating conditions that may warrant closer investigation. Further analysis would be needed to establish the factors associated with preventable incidents.

## Recommendations

Based on the metrics and analysis areas presented in the dashboards, the following actions could be considered:

- **Improve delivery visibility:** Examine on-time delivery performance by route, facility, and event type to identify recurring delay patterns.
- **Review fleet utilisation:** Investigate differences in utilisation and downtime across vehicles to identify areas for operational review.
- **Monitor operating costs:** Compare fuel and maintenance costs across vehicles and over time to identify unusual expenditure patterns.
- **Investigate route profitability:** Compare route-level revenue and profit to understand differences in financial contribution.
- **Strengthen safety analysis:** Examine preventable incidents by incident type and other available categories to identify potential areas for safety improvement.

These recommendations are proposed follow-up actions based on the dashboard metrics. Further analysis is needed to establish causes and determine which interventions would be most effective.

## Limitations and Considerations

The dashboard metrics describe the available dataset and should be interpreted within its scope. Additional investigation is required to establish the causes of delivery delays, maintenance expenditure, downtime, and safety incidents.

## Conclusion

This project involved preparing logistics data with SQL, developing DAX measures, and building four Power BI dashboard pages to analyse financial performance, driver safety, fleet efficiency, and delivery operations. The dashboards bring together key performance indicators to support comparisons across business areas and highlight opportunities for further investigation.

## Skills Demonstrated

- SQL querying and data transformation
- Text cleaning and field preparation
- Excel and Power Query
- Power BI dashboard development
- KPI reporting and data visualisation
- Operational and financial performance analysis
- Communicating findings and proposing evidence-based follow-up analysis

## Project Files

- **Power BI report (.pbix):** The Power BI report containing the four dashboard pages and associated DAX measures.
- **Dashboard screenshots:** Images of the four dashboard pages are available in the `assets` folder.
