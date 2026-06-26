# Chart Selection Justification
## Executive Sales Dashboard — Visualization Design Decisions

---

## 1. Sales Trend — Line Chart

**Question answered:** How are monthly sales changing over time?

**Why line chart:**
A line chart is the standard choice for time-series data. It shows continuity, direction, and momentum clearly. The eye naturally follows the line and detects peaks, troughs, and seasonal patterns. A bar chart would have worked but becomes cluttered with 24+ monthly bars.

**Fields used:**
- X axis: Order Date (continuous, monthly)
- Y axis: SUM(Sales)
- Color: Ship Mode (to show which mode drives sales each month)

**Design principle applied:** Continuity — line charts communicate trends better than discrete bars for time-based data.

**Mistake avoided:** Did not use a stacked area chart, which would have made individual ship mode trends hard to read.

---

## 2. Regional Performance — Horizontal Bar Chart

**Question answered:** Which region generates the highest sales?

**Why horizontal bar:**
Horizontal bars are ideal for comparing discrete categories (regions). Labels fit naturally on the left. Sorting bars from highest to lowest makes ranking immediately visible without reading every value.

**Fields used:**
- Rows: Region
- Columns: SUM(Sales)
- Label: SUM(Sales) value shown on bar

**Design principle applied:** Sorting — bars sorted descending so the best-performing region is always at the top, reducing cognitive load.

**Mistake avoided:** Did not use a pie chart, which makes comparing 4 regions harder and distorts perception of differences.

---

## 3. Category Profitability — Horizontal Bar Chart

**Question answered:** Which sub-categories drive profit and which cause losses?

**Why horizontal bar:**
Sub-category names are long and fit naturally on the Y axis. Bars extending left (negative profit) and right (positive profit) from a zero baseline clearly show profitable vs loss-making sub-categories at a glance.

**Fields used:**
- Rows: Sub Category
- Columns: SUM(Profit)
- Color: Category (Furniture, Office Supplies, Technology)
- Sorted: Descending by Profit

**Design principle applied:** Zero baseline — profit bars diverge from zero, making losses visually obvious without requiring the viewer to read exact numbers.

**Mistake avoided:** Did not truncate the axis — all bars start from zero to avoid misleading scale.

---

## 4. Customer Segment — Horizontal Bar Chart

**Question answered:** Which customer segment contributes most to sales and profit?

**Why horizontal bar:**
Only 3 segments to compare — a simple horizontal bar is clean and uncluttered. Adding profit as color encodes two metrics in one chart efficiently.

**Fields used:**
- Rows: Customer Segment
- Columns: SUM(Sales)
- Color: SUM(Profit)
- Label: Profit Margin %

**Design principle applied:** Dual encoding — bar length shows sales volume, color shows profitability, so leadership sees both dimensions at once.

**Mistake avoided:** Did not use a scatter plot here — too few data points (3 segments) to justify a scatter.

---

## 5. Shipping Performance — Horizontal Bar Chart

**Question answered:** Which shipping mode takes the longest and handles the most orders?

**Why horizontal bar:**
Ship mode names are readable on Y axis. Average delivery days as bar length gives an instant comparison. Order count as label adds a second insight without adding a second chart.

**Fields used:**
- Rows: Ship Mode
- Columns: AVG(Delivery Days)
- Color: Ship Mode
- Label: COUNTD(Order Id)

**Design principle applied:** Minimal clutter — two insights (speed + volume) in one chart instead of two separate charts.

**Mistake avoided:** Did not use SUM of delivery days, which would have been misleading (more orders = more total days regardless of speed).

---

## 6. Discount vs Profit — Scatter Plot

**Question answered:** Does higher discounting lead to lower profit?

**Why scatter plot:**
A scatter plot is the only chart type that clearly shows the relationship (correlation) between two continuous numerical variables. The downward trend from left to right directly answers whether discounting hurts profitability.

**Fields used:**
- Columns: AVG(Discount)
- Rows: AVG(Profit)
- Color: Category
- Detail: Sub Category (each dot = one sub-category)

**Design principle applied:** Appropriate chart for correlation — scatter is the correct tool for showing relationships between two measures.

**Mistake avoided:** Did not use a bar chart here, which cannot show the relationship between two continuous variables.

---

## 7. Return Analysis — Horizontal Bar Chart

**Question answered:** Which category has the highest return rate, and which segment drives returns?

**Why horizontal bar:**
Only 3 categories — a bar chart is clean and direct. Color by customer segment shows which segment drives returns within each category without adding complexity.

**Fields used:**
- Rows: Category
- Columns: Return Rate (calculated field)
- Color: Customer Segment
- Label: Return Rate value

**Design principle applied:** Segmentation within bars — stacked color shows segment breakdown without needing a separate chart.

**Mistake avoided:** Did not use Return Flag raw count — used Return Rate (proportion) instead, which accounts for different category volumes and gives a fair comparison.

---

## Overall Dashboard Design Principles Applied

| Principle | How Applied |
|-----------|-------------|
| Correct chart selection | Each chart matches its business question (trend=line, comparison=bar, correlation=scatter) |
| Clear hierarchy | KPI cards at top → charts below in logical reading order |
| Minimal clutter | Legends removed where redundant; gridlines minimized |
| Consistent color | Category always uses same color across all sheets |
| Proper labels | All charts show data labels for key values |
| Readable titles | Every sheet has a clear business-friendly title |
| Appropriate sorting | All bar charts sorted descending for instant ranking |
| Useful filters | Region, Category, Order Date filters apply across dashboard |
| No misleading scales | All axes start from zero; no truncated bars |
| Business interpretation | Chart titles state the business question, not just the field name |
