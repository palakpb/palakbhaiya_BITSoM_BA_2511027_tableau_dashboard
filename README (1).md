# Executive Sales Dashboard — Tableau
## Retail Chain Performance Analysis

---

## 1. Business Problem Summary
The leadership team of a retail chain needs a single executive dashboard to monitor sales performance, profitability, customer segments, category performance, shipping efficiency, discount impact, and return patterns across regions.

Key business questions:
- Which regions, categories, and segments drive the most sales and profit?
- Are discounts helping or hurting profitability?
- Which product categories carry the highest return risk?
- How is sales performance trending over time?
- Which shipping modes are delivering on their promise?

The dashboard is designed to help leadership identify opportunities, flag risks, and make data-backed decisions — not just view numbers.

---

## 2. Dataset Description
- **File**: `data/dashboard_sales_data.xlsx`
- **Key fields**:

| Field | Type | Description |
|-------|------|-------------|
| Order Date | Date | Date of order placement |
| Ship Date | Date | Date of shipment |
| Region | Dimension | Geographic region (East, West, North, South) |
| Category | Dimension | Product category (Furniture, Office Supplies, Technology) |
| Sub Category | Dimension | Product sub-category |
| Customer Segment | Dimension | Consumer, Corporate, Home Office |
| Ship Mode | Dimension | Standard, Second, First Class, Same Day |
| Campaign Channel | Dimension | Marketing channel |
| Sales | Measure | Revenue per transaction |
| Profit | Measure | Profit per transaction |
| Discount | Measure | Discount applied (0–1 decimal) |
| Quantity | Measure | Units sold |
| Delivery Days | Measure | Days between order and delivery |
| Return Flag | Measure | 1 = returned, 0 = not returned |
| Customer Rating | Measure | Customer satisfaction score |

---

## 3. Tableau Workbook Description
- **File**: `tableau/executive_dashboard.twbx`
- **Sheets**: 10 sheets (7 analysis views + 3 KPI cards)
- **Dashboard**: 1 executive dashboard combining all views
- **Interactions**: Filter actions, highlight actions, cross-chart filtering

**Sheets included:**
1. Sales Trend — line chart, monthly sales over time
2. Regional Performance — horizontal bar, sales by region
3. Category Profitability — horizontal bar, profit by sub-category
4. Customer Segment — horizontal bar, sales and margin by segment
5. Shipping Performance — horizontal bar, avg delivery days by ship mode
6. Discount vs Profit — scatter plot, discount vs profit relationship
7. Return Analysis — horizontal bar, return rate by category and segment
8. KPI - Total Sales
9. KPI - Total Profit
10. KPI - Return Rate

---

## 4. Calculated Fields Created

| Field Name | Formula | Purpose |
|------------|---------|---------|
| Profit Margin | `SUM([Profit]) / SUM([Sales])` | Measures profitability as a percentage of sales |
| Cost | `SUM([Sales]) - SUM([Profit])` | Derives cost from sales and profit |
| Avg Order Value | `SUM([Sales]) / COUNTD([Order Id])` | Average revenue per unique order |
| Return Rate | `SUM([Return Flag]) / COUNTD([Order Id])` | Proportion of orders returned |
| Shipping Delay Bucket | `IF [Delivery Days] <= 2 THEN "Fast" ELSEIF [Delivery Days] <= 5 THEN "Standard" ELSE "Delayed" END` | Categorizes delivery speed into meaningful buckets |

---

## 5. Dashboard Components

| Component | Type | Purpose |
|-----------|------|---------|
| KPI - Total Sales | Text card | Shows total revenue at a glance |
| KPI - Total Profit | Text card | Shows total profit at a glance |
| KPI - Return Rate | Text card | Shows overall return rate |
| Sales Trend | Line chart | Shows monthly sales trajectory over time |
| Regional Performance | Horizontal bar | Compares sales across 4 regions |
| Category Profitability | Horizontal bar | Shows profit/loss by sub-category |
| Customer Segment | Horizontal bar | Compares segment sales and margins |
| Shipping Performance | Horizontal bar | Compares delivery speed by ship mode |
| Discount vs Profit | Scatter plot | Shows discount-profit relationship |
| Return Analysis | Horizontal bar | Shows return rate by category and segment |

---

## 6. Filters and Interactions Used

| Filter | Type | Applied To |
|--------|------|-----------|
| Region | Dropdown | All charts on dashboard |
| Category | Dropdown | All charts on dashboard |
| Order Date | Date range | Sales Trend and all time-based views |

**Interactions:**
- Selecting a region in the Region filter updates all charts simultaneously
- Clicking a bar in Regional Performance highlights that region across other charts
- Date range filter controls the time window for all views

---

## 7. Key Business Insights

1. **Sales are growing** year-over-year with consistent Q4 peaks driven by seasonal demand
2. **East region leads** in total sales; South significantly underperforms relative to store count
3. **Technology (Copiers, Phones)** generates the highest profit; Furniture sub-categories (Tables, Bookcases) show negative profit
4. **Home Office segment** has the highest profit margin despite lowest sales volume
5. **Discounts above 20%** consistently result in negative profit across all categories
6. **Standard Class** handles 2,435 orders — the dominant shipping mode; Same Day delivery shows inconsistent performance
7. **Furniture has the highest return rate** — nearly double Technology's rate, adding hidden logistics costs
8. **Furniture is a triple risk** — negative profit + highest discounts + highest returns = immediate strategic review needed

---

## 8. Dashboard Story Summary

The dashboard reveals a business with genuine growth momentum being partially undermined by structural problems in the Furniture category and discount practices.

**Performing well:** Technology products, East and West regions, Home Office segment, Q4 seasonal demand capture.

**Underperforming:** South region, Furniture category (Tables, Bookcases), Same Day shipping fulfillment.

**Key risks:** Uncapped discounting destroying margins, Furniture losses compounded by high return costs, over-reliance on Q4 revenue.

**Key opportunities:** Grow Technology investment, develop Home Office loyalty program, fix South region performance, replicate West region efficiency model.

**Top recommended action:** Exit or reprice Tables and Bookcases immediately — they are the single largest profit drain in the business.

Full story: `outputs/dashboard_story.md`

---

## 9. Assumptions and Limitations

**Assumptions:**
- Return Flag = 1 means the order was returned; 0 means it was not
- Delivery Days is calculated as Ship Date minus Order Date
- Discount is stored as a decimal (0.20 = 20% discount)
- All monetary values are in the same currency (₹)

**Limitations:**
- Dashboard shows correlation, not causation — reducing discounts may not automatically improve profit
- No customer lifetime value data — a discounted sale to a loyal customer may still be profitable long-term
- Return reasons are unknown — high return rates need qualitative investigation
- No competitor benchmark — cannot determine if performance is above or below market
- Time period may include unusual demand patterns not representative of steady-state business

---