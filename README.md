# 📊 Superstore Sales Data Analysis

## 📝 Project Overview
This project analyzes **Superstore sales data** using **SQL Server/PostgreSQL** to extract key business insights.  
The goal is to identify **sales trends, customer behavior, and operational performance**, and visualize results using **Power BI**.

📂 **Project Deliverables:**
- **SQL Queries for Business Analysis** 📄
- **Insights & Recommendations** 💡
- **CSV Exports for Dashboarding** 📊
- **Power BI/Tableau Report** 📊

---

## **🔍 1. Data Exploration**
### **Check for NULL Values in All Columns**
```sql
SELECT
    column_name,
    COUNT(*) AS total_rows,
    SUM(CASE WHEN column_name IS NULL THEN 1 ELSE 0 END) AS missing_values
FROM sales_data
CROSS JOIN LATERAL (
    SELECT column_name
    FROM information_schema.columns
    WHERE table_name = 'sales_data'
) AS cols
GROUP BY column_name
ORDER BY missing_values DESC;
```
### **Checking for Duplicates**
```sql
SELECT row_id, COUNT(*) AS duplicate_count
FROM sales_data
GROUP BY row_id
HAVING COUNT(*) > 1;
```
## **📊 2. Business Performance Analysis**
### **Business Performance Metrics**
```sql
SELECT 
    SUM(sales) AS total_revenue,
    SUM(profit) AS total_profit,
    COUNT(DISTINCT order_id) AS total_orders,
	SUM(sales)/COUNT(DISTINCT order_id) AS avg_revenue_per_order,
	SUM(profit)/COUNT(DISTINCT order_id) AS avg_profit_per_order,
	(SUM(profit) / SUM(sales)) * 100 AS avg_margin_percentage
FROM sales_data;
```
### **Top 10 Best-Selling Products**
```sql
SELECT product_name,
    SUM(sales) AS total_sales
FROM sales_data
GROUP BY product_name
ORDER BY total_sales DESC
LIMIT 10;
```
### **Sales by Region**
```sql
SELECT region,
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit
FROM sales_data
GROUP BY region
ORDER BY total_sales DESC;
```
## **📈 3. Operational Insights**
### **Average Profit Margin**
```sql
SELECT SUM(profit) AS total_profit,
    SUM(sales) AS total_sales,
    (SUM(profit) / NULLIF(SUM(sales), 0)) * 100 AS avg_margin_percentage
FROM sales_data;
```
### **Impact of Discounts on Profitability**
```sql
SELECT discount,
    AVG(profit) AS avg_profit,
    COUNT(*) AS num_orders
FROM sales_data
GROUP BY discount
ORDER BY discount;
```
### **Impact of Discounts on Profitability**
```sql
SELECT discount,
    AVG(profit) AS avg_profit,
    COUNT(*) AS num_orders
FROM sales_data
GROUP BY discount
ORDER BY discount;
```
### **Average Shipping Time by Ship Mode**
```sql
SELECT ship_mode,
    AVG(CAST(ship_date AS DATE) - CAST(order_date AS DATE)) AS avg_delivery_days
FROM sales_data
WHERE ship_date IS NOT NULL AND order_date IS NOT NULL
GROUP BY ship_mode
ORDER BY avg_delivery_days;
```
## **📊 4. Power BI/Tableau Visualizations**
**Key Visualizations:**

* Sales Overview (Revenue, Profit, Orders)
* Monthly Sales Trends (Line Chart)
* Best-Selling Products (Bar Chart)
* Regional Performance (Map)
* Customer Segmentation (Pie Chart)

## **📌 Key Business Insights & Recommendations**
✅ Invest in High-Selling Categories:
* Office chairs & desks drive the most revenue.<br>

✅ Boost Q1 Sales with Promotions:<br>
* February sales slump → Offer New Year discounts.<br>

✅ Expand in Profitable Regions:<br>
* West region dominates sales but South has higher profit margins.<br>

✅ Leverage Corporate Clients:<br>
* Top spenders are business customers → Offer bulk discounts.<br>


## **🔗 Project Files**
📂 SQL Scripts: queries.sql<br>
📂 CSV Export: sales_data.csv<br>
📂 Power BI Report: Sales_Dashboard.pbix<br>

## **🏆 Final Thoughts**
💡 This project demonstrates:<br>
✔ SQL querying for data analysis & reporting<br>
✔ Business insights using real-world sales data<br>
✔ Power BI/Tableau dashboarding<br>

📌 Next Steps: Expand analysis with predictive modeling & customer churn analysis.

## **🚀 Connect With Me**
🔗 [LinkedIn](https://www.linkedin.com/in/kyle-darden/)<br>
📊 [GitHub](https://github.com/dardenkyle)<br>
📧 darden_kyle@hotmail.com <br>