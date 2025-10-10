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

---

## Objective
The main objective of this project is to help Apple’s retail division optimize its product and customer strategies by:
- Detecting low-performing products across countries.  
- Evaluating after-sales reliability through warranty claims.  
- Recognizing seasonal sales peaks for better inventory management.  
- Identifying high-claim product categories to improve quality and service design.

---

## Data Dictionary

**stores:** Contains information about Apple retail stores.  
- store_id: Unique identifier for each store.  
- store_name: Name of the store.  
- city: City where the store is located.  
- country: Country of the store.  

**category:** Holds product category information.  
- category_id: Unique identifier for each product category.  
- category_name: Name of the category.  

**products:** Details about Apple products.  
- product_id: Unique identifier for each product.  
- product_name: Name of the product.  
- category_id: References the category table.  
- launch_date: Date when the product was launched.  
- price: Price of the product.  

**sales:** Stores sales transactions.  
- sale_id: Unique identifier for each sale.  
- sale_date: Date of the sale.  
- store_id: References the store table.  
- product_id: References the product table.  
- quantity: Number of units sold.  

**warranty:** Contains information about warranty claims.  
- claim_id: Unique identifier for each warranty claim.  
- claim_date: Date the claim was made.  
- sale_id: References the sales table.  
- repair_status: Status of the warranty claim (e.g., Paid, Repaired, Warranty Void).

---

## Data Preparation and Methodology

1. **Data Quality Checks**  
   - Ensured all relationships between tables (foreign keys) were valid.  
   - Verified no duplicate sales or warranty claims existed.  
   - Checked for missing or invalid data in key columns such as dates and quantities.

2. **Feature Engineering**  
   - Extracted `year` and `month` from `sale_date` for easier time-based analysis.  
   - Calculated the number of days between each `sale_date` and `claim_date` to analyze warranty timing.  
   - Joined all tables into a single dataset that combines sales, stores, products, and warranty details.

3. **Analytical Approach**  
   - Used SQL aggregate functions (`SUM`, `COUNT`, `GROUP BY`) to compute key metrics.  
   - Applied date filters to focus on recent and relevant timeframes.  

---

## Key Findings

### 1. Least Selling Product by Country and Year
```sql
SELECT country, p.product_name, EXTRACT(YEAR FROM s.sale_date) AS year,
       SUM(s.quantity) AS total_units_sold
FROM sales s
JOIN stores st ON s.store_id = st.store_id
JOIN products p ON s.product_id = p.product_id
GROUP BY country, p.product_name, year
ORDER BY total_units_sold ASC;
---
```
### 2. Warranty Claims within 180 Days
```sql
SELECT COUNT(w.claim_id) AS claims_within_180_days
FROM warranty w
JOIN sales s ON w.sale_id = s.sale_id
WHERE (w.claim_date - s.sale_date) <= 180;

```
---

### 3. Warranty Claims for Recently Launched Products
```sql
SELECT COUNT(w.claim_id) AS recent_product_claims
FROM warranty w
JOIN sales s ON w.sale_id = s.sale_id
JOIN products p ON s.product_id = p.product_id
WHERE p.launch_date >= CURRENT_DATE - INTERVAL '2 years';
```
---

### 4. High-Sales Months in the USA
```sql
SELECT EXTRACT(YEAR FROM s.sale_date) AS year,
       EXTRACT(MONTH FROM s.sale_date) AS month,
       SUM(s.quantity) AS total_units
FROM sales s
JOIN stores st ON s.store_id = st.store_id
WHERE st.country = 'USA'
  AND s.sale_date >= CURRENT_DATE - INTERVAL '3 years'
GROUP BY year, month
HAVING SUM(s.quantity) > 5000
ORDER BY year, month;
```

---

### 5. Product Category with Most Warranty Claims
```sql
SELECT c.category_name, COUNT(w.claim_id) AS total_claims
FROM warranty w
JOIN sales s ON w.sale_id = s.sale_id
JOIN products p ON s.product_id = p.product_id
JOIN category c ON p.category_id = c.category_id
WHERE w.claim_date >= CURRENT_DATE - INTERVAL '2 years'
GROUP BY c.category_name
ORDER BY total_claims DESC
LIMIT 1;
```
---

## Insights and Recommendations

| Area | Insight | Recommendation |
|------|----------|----------------|
| Product Portfolio | Older accessories have weak sales | Discontinue or reposition these products |
| Quality Control | Early warranty claims are high | Strengthen pre-launch testing |
| Launch Strategy | New products show above-average claim rates | Implement extended testing cycles |
| Sales Planning | Clear seasonal peaks in USA | Align stock and campaigns with sales cycles |
| After-Sales Service | Wearables have high claim volume | Improve repair service and customer experience |
