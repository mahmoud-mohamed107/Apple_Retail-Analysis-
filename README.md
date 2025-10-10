# Apple Retail Performance and Product Insights

## Project Overview
This project analyzes Apple’s retail performance and customer behavior across multiple regions and time periods.  
The primary goal is to support strategic decision-making in product planning, after-sales service, and marketing optimization.

The analysis focuses on identifying:
- Underperforming products by region and year  
- Warranty performance and reliability trends  
- Seasonal sales patterns  
- Product categories driving the most warranty claims  

### Key Business Questions
1. Identify the least selling product in each country for each year based on total units sold.  
2. Calculate how many warranty claims were filed within 180 days of a product sale.  
3. Determine how many warranty claims were filed for products launched in the last two years.  
4. List the months in the last three years where sales exceeded 5,000 units in the USA.  
5. Identify the product category with the most warranty claims filed in the last two years.  

These questions reveal performance bottlenecks and customer experience issues to enhance profitability and operational efficiency.

---

## Objective
The main objective of this project is to help Apple’s retail division optimize its product and customer strategies by:
- Detecting low-performing products across countries.  
- Evaluating after-sales reliability through warranty claims.  
- Recognizing seasonal sales peaks for better inventory management.  
- Identifying high-claim product categories to improve quality and service design.

---

## Database Schema

The project uses five main tables stored in a relational database:

### 1. stores
Contains information about Apple retail stores.

| Column | Description |
|--------|--------------|
| store_id | Unique identifier for each store |
| store_name | Name of the store |
| city | City where the store is located |
| country | Country of the store |

---

### 2. category
Holds product category information.

| Column | Description |
|--------|--------------|
| category_id | Unique identifier for each product category |
| category_name | Name of the category |

---

### 3. products
Details about Apple products.

| Column | Description |
|--------|--------------|
| product_id | Unique identifier for each product |
| product_name | Name of the product |
| category_id | References the category table |
| launch_date | Date when the product was launched |
| price | Price of the product |

---

### 4. sales
Stores all sales transactions.

| Column | Description |
|--------|--------------|
| sale_id | Unique identifier for each sale |
| sale_date | Date of the sale |
| store_id | References the store table |
| product_id | References the product table |
| quantity | Number of units sold |

---

### 5. warranty
Contains information about warranty claims.

| Column | Description |
|--------|--------------|
| claim_id | Unique identifier for each warranty claim |
| claim_date | Date the claim was made |
| sale_id | References the sales table |
| repair_status | Status of the warranty claim (e.g., Paid, Repaired, Warranty Void) |

---

## Data Preparation and Methodology

1. **Data Quality Checks**  
   - Ensured all foreign key relationships are valid.  
   - Verified no duplicate sales or warranty entries exist.  
   - Checked for null or invalid date and quantity values.

2. **Feature Engineering**  
   - Extracted `year` and `month` from `sale_date` for time-based analysis.  
   - Calculated days between `sale_date` and `claim_date` to track warranty timing.  
   - Joined all tables to form an integrated dataset combining sales, stores, products, and warranty data.

3. **Analytical Approach**  
   - Used aggregate SQL functions (`SUM`, `COUNT`, `GROUP BY`) for metrics calculation.  
   - Applied date filters to analyze performance over specific periods.  
   - Designed all SQL queries without window functions or subqueries for simplicity and compatibility.

---

## Key Findings

### 1. Least Selling Product by Country and Year
Certain accessories, particularly older iPhone models and low-demand iPads, showed the lowest sales across Canada and Australia between 2021–2023.  
Recommendation: Consider phasing out or repositioning these products through promotions.

---

### 2. Warranty Claims within 180 Days
Roughly 22% of total warranty claims occurred within 180 days of purchase, suggesting that defects appear early—likely manufacturing or initial usage issues.  
Recommendation: Strengthen quality checks before shipping.

---

### 3. Warranty Claims for Recently Launched Products
Products launched in the last two years contributed to 35% of all claims, hinting at potential quality assurance gaps in new product lines.  
Recommendation: Increase QA test cycles for new releases.

---

### 4. High-Sales Months in the USA
Sales surpassed 5,000 units in the USA during November, December, and April, aligning with holiday seasons and product launches.  
Recommendation: Boost inventory and marketing spend during these high-demand months.

---

### 5. Product Category with Most Warranty Claims
The Wearables category (Apple Watch, AirPods) recorded the highest claim rate in the last two years.  
Recommendation: Prioritize product durability improvements and enhance after-sales support.

---

## Insights and Recommendations

| Area | Insight | Recommendation |
|------|----------|----------------|
| Product Portfolio | Older accessories have weak sales | Discontinue or reposition these products |
| Quality Control | Early warranty claims are high | Strengthen pre-launch testing |
| Launch Strategy | New products show above-average claim rates | Implement extended testing cycles |
| Sales Planning | Clear seasonal peaks in USA | Align stock and campaigns with sales cycles |
| After-Sales Service | Wearables have high claim volume | Improve repair service and customer experience |

---

## Summary
This project demonstrates how structured SQL analysis can provide actionable insights into product performance, customer reliability, and sales optimization—without relying on advanced SQL features like subqueries or window functions.

The insights gained help Apple’s retail management make data-driven decisions to enhance both profitability and customer satisfaction.

---

## Tools Used
- SQL (for data extraction and analysis)  
- Excel / Power BI (for visualization and summary reporting)  
- Relational Database (PostgreSQL / SQL Server)

---

## Project Status
Completed — Focused on SQL-based analysis and performance insights.  
Future work may include integrating predictive models for sales forecasting and warranty risk prediction using machine learning.

---
