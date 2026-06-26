Executive Sales Dashboard — Tableau

Retail Chain Performance Analysis

1. Business Problem Summary

The leadership team of a retail chain needs a single executive dashboard to monitor sales performance, profitability, customer segments, category performance, shipping efficiency, discount impact, and return patterns across regions.

Key business questions:

Which regions, categories, and segments drive the most sales and profit?
Are discounts helping or hurting profitability?
Which product categories carry the highest return risk?
How is sales performance trending over time?
Which shipping modes are delivering on their promise?

The dashboard is designed to help leadership identify opportunities, flag risks, and make data-backed decisions — not just view numbers.

2. Dataset Description

File: data/dashboard_sales_data.xlsx
Key fields:

FieldTypeDescriptionOrder DateDateDate of order placementShip DateDateDate of shipmentRegionDimensionGeographic region (East, West, North, South)CategoryDimensionProduct category (Furniture, Office Supplies, Technology)Sub CategoryDimensionProduct sub-categoryCustomer SegmentDimensionConsumer, Corporate, Home OfficeShip ModeDimensionStandard, Second, First Class, Same DayCampaign ChannelDimensionMarketing channelSalesMeasureRevenue per transactionProfitMeasureProfit per transactionDiscountMeasureDiscount applied (0–1 decimal)QuantityMeasureUnits soldDelivery DaysMeasureDays between order and deliveryReturn FlagMeasure1 = returned, 0 = not returnedCustomer RatingMeasureCustomer satisfaction score


3. Tableau Workbook Description


File: tableau/executive_dashboard.twbx
Sheets: 10 sheets (7 analysis views + 3 KPI cards)
Dashboard: 1 executive dashboard combining all views
Interactions: Filter actions, highlight actions, cross-chart filtering


Sheets included:
Sales Trend — line chart, monthly sales over time
Regional Performance — horizontal bar, sales by region
Category Profitability — horizontal bar, profit by sub-category
Customer Segment — horizontal bar, sales and margin by segment
Shipping Performance — horizontal bar, avg delivery days by ship mode
Discount vs Profit — scatter plot, discount vs profit relationship
Return Analysis — horizontal bar, return rate by category and segment
KPI - Total Sales
KPI - Total Profit
KPI - Return Rate

4. Calculated Fields Created

Field NameFormulaPurposeProfit MarginSUM([Profit]) / SUM([Sales])Measures profitability as a percentage of salesCostSUM([Sales]) - SUM([Profit])Derives cost from sales and profitAvg Order ValueSUM([Sales]) / COUNTD([Order Id])Average revenue per unique orderReturn RateSUM([Return Flag]) / COUNTD([Order Id])Proportion of orders returnedShipping Delay BucketIF [Delivery Days] <= 2 THEN "Fast" ELSEIF [Delivery Days] <= 5 THEN "Standard" ELSE "Delayed" ENDCategorizes delivery speed into meaningful buckets


5. Dashboard Components

ComponentTypePurposeKPI - Total SalesText cardShows total revenue at a glanceKPI - Total ProfitText cardShows total profit at a glanceKPI - Return RateText cardShows overall return rateSales TrendLine chartShows monthly sales trajectory over timeRegional PerformanceHorizontal barCompares sales across 4 regionsCategory ProfitabilityHorizontal barShows profit/loss by sub-categoryCustomer SegmentHorizontal barCompares segment sales and marginsShipping PerformanceHorizontal barCompares delivery speed by ship modeDiscount vs ProfitScatter plotShows discount-profit relationshipReturn AnalysisHorizontal barShows return rate by category and segment


6. Filters and Interactions Used

FilterTypeApplied ToRegionDropdownAll charts on dashboardCategoryDropdownAll charts on dashboardOrder DateDate rangeSales Trend and all time-based views

Interactions:


Selecting a region in the Region filter updates all charts simultaneously
Clicking a bar in Regional Performance highlights that region across other charts
Date range filter controls the time window for all views



7. Key Business Insights


Sales are growing year-over-year with consistent Q4 peaks driven by seasonal demand
East region leads in total sales; South significantly underperforms relative to store count
Technology (Copiers, Phones) generates the highest profit; Furniture sub-categories (Tables, Bookcases) show negative profit
Home Office segment has the highest profit margin despite lowest sales volume
Discounts above 20% consistently result in negative profit across all categories
Standard Class handles 2,435 orders — the dominant shipping mode; Same Day delivery shows inconsistent performance
Furniture has the highest return rate — nearly double Technology's rate, adding hidden logistics costs
Furniture is a triple risk — negative profit + highest discounts + highest returns = immediate strategic review needed



8. Dashboard Story Summary

The dashboard reveals a business with genuine growth momentum being partially undermined by structural problems in the Furniture category and discount practices.

Performing well: Technology products, East and West regions, Home Office segment, Q4 seasonal demand capture.

Underperforming: South region, Furniture category (Tables, Bookcases), Same Day shipping fulfillment.

Key risks: Uncapped discounting destroying margins, Furniture losses compounded by high return costs, over-reliance on Q4 revenue.

Key opportunities: Grow Technology investment, develop Home Office loyalty program, fix South region performance, replicate West region efficiency model.

Top recommended action: Exit or reprice Tables and Bookcases immediately — they are the single largest profit drain in the business.

Full story: outputs/dashboard_story.md


9. Assumptions and Limitations

Assumptions:


Return Flag = 1 means the order was returned; 0 means it was not
Delivery Days is calculated as Ship Date minus Order Date
Discount is stored as a decimal (0.20 = 20% discount)
All monetary values are in the same currency (₹)


Limitations:


Dashboard shows correlation, not causation — reducing discounts may not automatically improve profit
No customer lifetime value data — a discounted sale to a loyal customer may still be profitable long-term
Return reasons are unknown — high return rates need qualitative investigation
No competitor benchmark — cannot determine if performance is above or below market
Time period may include unusual demand patterns not representative of steady-state business
