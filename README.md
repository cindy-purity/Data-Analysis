# E-Commerce Sales Analysis: African Market Performance (2024)
# Introduction

This project analyzes sales data from a fictional African e-commerce retailer 
covering January to July 2024. The raw dataset contained 70 orders across 4 product 
categories, 5 regions, and 5 sales reps.

Before analysis, the data was cleaned using DuckDB SQL to resolve inconsistent date 
formats, mixed text casing, NULL values, a duplicate order, and one outlier entry. 
All analysis was performed on the cleaned table `sales_clean`.

The goal is to uncover patterns in revenue, customer behavior, product performance, 
and operational efficiency that can inform business decisions.

# Data Cleaning  Exploratory Analysis with SQL

The raw dataset had several quality issues fixed before analysis using a single 
DuckDB SQL query saved as `sales_clean`.

- **Date formats:** Four mixed formats standardized to `YYYY-MM-DD` using `strptime()`
- **Text casing:** All text fields lowercased using `LOWER()` for consistency
- **NULL values:** Missing emails and regions replaced with `'unknown'` via `COALESCE()`. 
  NULL ship dates were retained intentionally as they represent unshipped or cancelled orders
- **Discounts:** NULL discount values replaced with `0`

# Exploratory Analysis with SQL

## Revenue by Region

West Africa leads with KES 447,695 in total revenue, followed closely by East Africa. 
Southern Africa contributes a smaller share. South Asia was excluded from regional 
analysis as it falls outside the core market.

## Average Revenue by Product Category

ORD-1061 was excluded as a data entry error (quantity of 100 units on a single order).

Fashion leads average order value at KES 6,114 but with only 13 orders. 
Electronics follows at KES 4,306 but dominates in volume with 27 orders. 
Beauty is the weakest performer at KES 2,939 per order.

## Total Revenue by Product Category

Electronics drives the most total revenue at KES 116,260, proving that 
consistent volume beats high ticket size. Fashion (KES 79,485) and 
Home & Kitchen (KES 77,210) are close. Beauty trails at KES 41,150.


## Sales Rep Performance

Linda Asante leads with 24 orders and KES 123,705 in revenue. James Otieno 
follows with 19 orders and KES 88,960. Together they account for over 67% 
of total revenue, which is a concentration risk worth monitoring. Felix Nair's 
2 orders reflect his out-of-scope regional coverage, not underperformance.

## Order Status

90% of orders were delivered successfully. 3 were cancelled and 4 are still 
processing with no ship date assigned, which should be reviewed.

## Top 5 Customers by Total Spend

**Alice Mwangi** is the highest spending customer at **KES 17,100**, 
followed by **Grace Mutua** at **KES 13,600**. Both are repeat customers 
which explains their higher totals. The remaining three, Rahim Patel, 
Eunice Mwamba, and Victor Mensah, range between KES 9,120 and KES 11,000. 
Repeat customers like Alice and Grace are worth prioritizing for loyalty 
initiatives since retaining them costs less than acquiring new ones.

_Note: ORD-1061 was excluded from this analysis as it contained an anomalous quantity of 100 units on a single order, identified as a likely data entry error._

## Average Shipping Time

On average, orders are shipped within **2.6 days** of being placed. 
That is a fast turnaround and reflects well on the fulfillment operation.

Note: Cancelled and processing orders were excluded from this calculation 
as they have no ship date. Including them would have skewed the average.

## Monthly Sales Trend

April was the strongest month with **12 orders** and **KES 57,085** in revenue, 
followed closely by May at KES 52,190. January through March were consistent, 
hovering around KES 48,000 per month. June dipped slightly and July shows only 
3 orders and KES 15,700, but this is expected since the dataset only covers 
the first two weeks of July and is not a full month of data.

## Open Orders with No Ship Date

4 orders are still in Processing status with no ship date assigned. 
The oldest is ORD-1006 from January 18th, meaning it has been sitting 
open for nearly 6 months. All four should be investigated and either 
fulfilled or cancelled to keep the order book clean.

# Conclusion and Recommendations

This analysis covered revenue by region and category, sales rep performance, 
customer spend, shipping efficiency, and monthly trends across 68 valid orders.

**Key findings:**
- Electronics drives the most total revenue through consistent volume
- Fashion has the highest average order value but low and inconsistent order frequency
- West Africa and East Africa are the core markets
- Linda Asante and James Otieno account for over 67% of total revenue
- Average shipping time is 2.6 days, indicating a healthy fulfillment operation
- 4 orders have been sitting in Processing status with no ship date, the oldest since January

**Recommendations:**
- Investigate and resolve the 4 open processing orders immediately
- Monitor dependence on Linda and James by developing the rest of the sales team
- Run a targeted campaign to increase Fashion order frequency given its high ticket size
- Invest further in Home & Kitchen which is a consistent and underrated performer
- Exclude or investigate ORD-1061 with the business before publishing any Fashion metrics
