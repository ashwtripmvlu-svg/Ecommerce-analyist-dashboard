1. Project Title
E-Commerce Customer Segmentation, Sales and Delivery Analytics Dashboard using Tableau
2. Objectives
•	Analyze customer purchasing patterns using order frequency and monetary value.
•	Apply Tableau clustering to segment customers and visually identify high-spending customers.
•	Compare sales by platform and product category.
•	Analyze delivery time, delivery delays, service ratings and refund requests.
•	Create an interactive dashboard with filters, KPI cards, a line-chart area, customer scatter plot and supporting charts.
•	Explore historical sales forecasting and moving averages if a valid order-date field is available.
3. Project Description
This project uses Tableau to analyze e-commerce order activity across Blinkit, JioMart and Swiggy Instamart. The dashboard combines sales KPIs, product-category analysis, platform comparison, customer frequency and monetary value, customer clustering, delivery performance, refunds and delays. Filters allow users to explore subsets of the data. The project uses only the columns present in the supplied CSV; fields that are not available, such as profit/cost and a valid calendar date, are not treated as measured facts.
4. Dataset Details
Parameter	Details
Dataset file	Ecommerce_Delivery_Analytics_New.csv
Source	User-provided CSV file
Records / rows	100,000 orders
Columns	11
Distinct orders	100,000
Distinct customers	9,000
Missing values	0 missing cells found in the supplied file
Sales field	Order Value (INR)
Platforms	Blinkit, JioMart, Swiggy Instamart
Product categories	Beverages, Dairy, Fruits & Vegetables, Grocery, Personal Care, Snacks
Important fields	Order ID, Customer ID, Platform, Order Date & Time, Delivery Time (Minutes), Product Category, Order Value (INR), Customer Feedback, Service Rating, Delivery Delay, Refund Requested

5. Data Quality Notes (Read Before Submission)
•	Order Date & Time is stored as text and has only 60 distinct values (examples include “19:29.5” and “54:29.5”). It does not provide a valid calendar date/time sequence. A real historical line trend, seasonal comparison or forecast cannot be reliably produced from this field as supplied.
•	The dataset has no Profit, Cost, Margin or Quantity column. Therefore, a true Profit Ratio, Total Profit and Total Quantity cannot be calculated from this file. Do not label refund status or sales as profit.
•	For this submission, use Order Value (INR) as sales/order value. Use “Sales by Order Minute/Time Text” only if needed for a demonstration and clearly label it as a proxy, not a time-series trend.
•	For proper forecasting, obtain a corrected dataset with an actual date field (for example, 2026-01-15 19:29:05). For Profit Ratio, add Profit or Cost (INR) data from a reliable source.
6. Tools and Technologies
•	Tableau Desktop or Tableau Public
•	CSV dataset: Ecommerce_Delivery_Analytics_New.csv
•	Tableau calculated fields, filters, clustering, dashboard actions and visual analytics
7. Data Summary and Calculated Results
Metric	Calculated result
Total order value / sales	₹59,099,440
Distinct orders	100,000
Distinct customers	9,000
Average order value	₹590.99
Average orders per customer	11.11
Average delivery time	29.54 minutes
Orders marked delayed	13,672 (13.67%)
Orders with refund requested	45,819 (45.82%)

Sales by Platform
Platform	Order value (INR)	Share of total
Swiggy Instamart	₹19,831,984	33.56%
Blinkit	₹19,705,084	33.34%
JioMart	₹19,562,372	33.10%

Sales by Product Category
Product category	Order value (INR)	Share of total
Personal Care	₹17,395,601	29.43%
Grocery	₹14,194,055	24.02%
Beverages	₹9,086,669	15.38%
Dairy	₹7,610,522	12.88%
Fruits & Vegetables	₹6,246,517	10.57%
Snacks	₹4,566,076	7.73%

Average Delivery Time by Platform
Platform	Average delivery time
Blinkit	29.47 minutes
JioMart	29.63 minutes
Swiggy Instamart	29.50 minutes

Top 5 Customers by Total Order Value
Customer ID	Total order value
CUST9682	₹16,255
CUST1605	₹16,185
CUST9084	₹15,547
CUST5386	₹15,467
CUST2175	₹15,209

8. Tableau Calculated Fields
Total Sales — Sum of order values; this is the main sales KPI.
SUM([Order Value (INR)])
Total Orders — Distinct number of orders.
COUNTD([Order ID])
Total Customers — Distinct number of customers.
COUNTD([Customer ID])
Average Order Value — Average order value.
AVG([Order Value (INR)])
Customer Frequency — Number of distinct orders for each customer. Use this as a customer-level measure.
{ FIXED [Customer ID] : COUNTD([Order ID]) }
Customer Monetary Value — Total order value for each customer.
{ FIXED [Customer ID] : SUM([Order Value (INR)]) }
Delayed Order Flag — Can be averaged and formatted as a percentage to show delay rate.
IF [Delivery Delay] = "Yes" THEN 1 ELSE 0 END
Refund Request Flag — Can be averaged and formatted as a percentage to show refund-request rate.
IF [Refund Requested] = "Yes" THEN 1 ELSE 0 END
Do not create a Profit Ratio from this dataset: the required Profit and Cost fields are absent. Do not create true Recency or forecast fields from the current Order Date & Time text. Once a real order timestamp is supplied, Recency can be calculated as the number of days between the latest date in the dataset and each customer’s last order date.
9. Tableau Worksheets: Step-by-Step Instructions
A. Connect the CSV
1.	Open Tableau Desktop / Tableau Public.
2.	Under Connect, choose Text File and select Ecommerce_Delivery_Analytics_New.csv.
3.	On the Data Source page, check the field names and data types. Keep Order ID and Customer ID as dimensions; Order Value (INR) and Delivery Time (Minutes) as numeric measures.
4.	Do not set Order Date & Time as a true Date unless you first correct the source values.
B. Create KPI cards
5.	Create one worksheet for each KPI: Total Sales, Total Orders, Total Customers and Average Order Value.
6.	Drag the corresponding calculated field/measure to Text on the Marks card.
7.	Format sales and average order value as Indian rupees; format order/customer counts with thousands separators.
8.	Use short sheet titles so the KPI cards fit across the dashboard.
C. Sales by Platform
9.	Create a new worksheet named Sales by Platform.
10.	Drag Platform to Columns and Order Value (INR) to Rows.
11.	Keep aggregation as SUM, choose Bar marks, sort descending and turn on mark labels.
D. Sales by Product Category
12.	Create a worksheet named Sales by Category.
13.	Drag Product Category to Rows and SUM(Order Value (INR)) to Columns.
14.	Sort descending, show labels and use a horizontal bar chart for readable category names.
E. Customer frequency and monetary value
15.	Create the Customer Frequency and Customer Monetary Value calculated fields above.
16.	Create a worksheet named Customer Segmentation. Drag Customer Frequency to Columns and Customer Monetary Value to Rows.
17.	Drag Customer ID to Detail on the Marks card and select Circle.
18.	Drag Customer Monetary Value to Size. Optionally drag Service Rating or Platform to Color if it makes the view easier to interpret.
19.	Open the Analytics pane and drag Cluster onto the scatter plot. Use 3 or 4 clusters as a starting point, then inspect the cluster centers and values before assigning business labels.
20.	Interpret clusters using actual values: high frequency/high monetary value, frequent lower spend, occasional higher spend, and lower frequency/lower spend. These labels are interpretations, not automatic facts.
F. Top 10 High-Value Customers
21.	Create a worksheet named Top 10 Customers.
22.	Drag Customer ID to Rows and Customer Monetary Value to Columns.
23.	Right-click Customer ID, choose Filter, then Top. Select Top 10 by SUM(Customer Monetary Value) (or use the FIXED LOD measure carefully).
24.	Sort descending and display the customer ID and value labels.
G. Delivery, delay and refund analysis
25.	Average Delivery Time by Platform: Platform to Columns; AVG(Delivery Time (Minutes)) to Rows.
26.	Delivery Delay: Delivery Delay to Columns; COUNTD(Order ID) to Rows.
27.	Refund Analysis: Refund Requested to Columns; COUNTD(Order ID) to Rows.
28.	Service Rating: Service Rating to Columns; COUNTD(Order ID) to Rows.
29.	Use bar charts and labels; these views describe delivery/service patterns, not profit.
H. Filters
30.	Add Platform, Product Category, Service Rating, Delivery Delay and Refund Requested to Filters.
31.	For each filter, choose Show Filter.
32.	On the dashboard, open the filter menu and choose Apply to Worksheets → All Using This Data Source.
33.	Use concise filter cards and place them in a single row near the top of the dashboard.
I. Build the dashboard
34.	Choose Dashboard → New Dashboard. Set a desktop size around 1366 × 768 or use Automatic.
35.	Place the dashboard title at the top. Place four KPI cards in one row.
36.	Place filters directly below the KPIs.
37.	Middle row: Sales by Platform, Sales by Category and Refund/Delay analysis.
38.	Bottom row: Customer Segmentation scatter plot and Top 10 Customers. Add Average Delivery Time if space permits.
39.	Click the cluster chart and select Use as Filter if appropriate. Test that other charts respond to the selection.
40.	Hide unnecessary legends, avoid truncated titles, and use consistent fonts and colors.
J. Forecasting and moving averages (requires corrected dates)
The current file cannot support a valid time-series forecast because Order Date & Time is malformed text with 60 distinct values, not a calendar date. Do not interpret the existing single-point forecast view as a valid forecast. After replacing this field with a real timestamp: place MONTH(Order Date) or WEEK(Order Date) on Columns, SUM(Order Value (INR)) on Rows, choose Line marks, then open Analytics and drag Forecast onto the view. To compare a moving average, right-click the sales measure and choose Quick Table Calculation → Moving Average. For seasonality, compare monthly sales across multiple years. Forecasting and seasonality should only be reported when valid historical dates and enough time periods are present.
10. Recommended Dashboard Layout
Area	Contents
Header	E-Commerce Customer Segmentation & Sales Analytics
KPI row	Total Sales | Total Orders | Total Customers | Average Order Value
Filter row	Platform | Product Category | Service Rating | Delivery Delay | Refund Requested
Middle left	Sales by Platform / Sales by Category
Middle right	Refund and Delivery Delay Analysis
Bottom left	Customer Segmentation scatter plot with Tableau clusters
Bottom right	Top 10 High-Value Customers and Average Delivery Time by Platform
Optional only after date correction	Sales line chart, moving average, monthly seasonal comparison and forecast

11. Dashboard Screenshots
The screenshots below show the current Tableau workbook state. Review the layout and correct the listed issues before final submission: the KPI titles/containers are too narrow in the overview screenshot, and the forecasting sheet in the cluster dashboard is not a valid forecast because the source date field is not a valid date.

 
Figure 1. Current overview dashboard screenshot.

 
Figure 2. Current customer cluster dashboard screenshot.
12. Key Insights from the Supplied Dataset
41.	Total order value across 100,000 orders is ₹59,099,440, with an average order value of ₹590.99.
42.	Swiggy Instamart has the highest platform order value at ₹19,831,984 (33.56% of total), followed closely by Blinkit and JioMart.
43.	Personal Care is the highest-value category at ₹17,395,601; Snacks is the lowest at ₹4,566,076.
44.	13,672 orders (13.67%) are marked delayed. The average delivery time by platform is approximately 29.5–29.6 minutes.
45.	45,819 orders (45.82%) have Refund Requested = Yes. Investigate refund reasons and customer feedback before drawing conclusions about service quality.
Customer segmentation note: customers average about 11.11 orders each; the customer with the highest total order value in this file is CUST9682 at ₹16,255. Use the Tableau clusters to group customers, then validate the cluster profile before naming each segment.
13. Conclusion
The dashboard supports interactive analysis of order value, platform and category performance, customer purchasing frequency, customer monetary value, customer clusters, delivery time, delays, ratings and refund requests. The most important data limitations are the missing profit/cost fields and the invalid order timestamp. The dashboard should be described as customer segmentation and sales/delivery analytics until a corrected date field is supplied for forecasting and reliable historical trends.
