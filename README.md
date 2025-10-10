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

## Database Schema (Simplified Explanation)

The dataset consists of **five main tables** that represent Apple’s retail and warranty operations.  
Below is a simple description of each table and what kind of information it contains.

### 1. Stores Table
This table contains basic information about each Apple retail store around the world.  
It includes:
- **Store ID:** A unique code for every store.  
- **Store Name:** The name used to identify the branch.  
- **City and Country:** The location details of the store.  

Essentially, it helps us understand *where* each sale happened.

---

### 2. Category Table
This is a short reference table that lists all the product categories.  
For example: “iPhone,” “iPad,” “Mac,” “Accessories,” “Wearables.”  
Each category has:
- **Category ID** — the code used to link it to products.  
- **Category Name** — the readable name of the product group.

This table helps group different products under one umbrella for analysis.

---

### 3. Products Table
This table stores all the details about Apple products themselves.  
It includes:
- **Product ID:** The unique code for each item (like iPhone 14 Pro, iPad Mini, etc.).  
- **Product Name:** The full name of the product.  
- **Category ID:** A reference that links the product to its category (from the Category table).  
- **Launch Date:** The date the product was officially released.  
- **Price:** The selling price of the product.

This table is the main reference for analyzing what was sold and when it was launched.

---

### 4. Sales Table
This is one of the core tables in the analysis — it records every sale transaction.  
Each row represents a specific sale and contains:
- **Sale ID:** The transaction number.  
- **Sale Date:** When the sale occurred.  
- **Store ID:** Where the sale took place.  
- **Product ID:** Which product was sold.  
- **Quantity:** How many units were sold in that transaction.

This table connects the **stores** and **products** tables and lets us calculate total sales per product, per region, or per year.

---

### 5. Warranty Table
This table contains all information related to warranty claims submitted by customers.  
Each record represents a single claim and includes:
- **Claim ID:** The unique number for each warranty claim.  
- **Claim Date:** When the customer submitted the claim.  
- **Sale ID:** A link to the specific sale transaction (from the Sales table).  
- **Repair Status:** Whether the claim was “Paid,” “Repaired,” or “Warranty Void.”

This table is essential for understanding product reliability and customer satisfaction.

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
   - Avoided using complex SQL features (like subqueries or window functions) for better portability.

---

## Key Findings

### 1. Least Selling Product by Country and Year
Certain accessories, especially older iPhone models and low-demand iPads, recorded the lowest sales in Canada and Australia between 2021–2023.  
**Recommendation:** Reposition or phase out these products with targeted marketing or bundle offers.

---

### 2. Warranty Claims within 180 Days
Around 22% of warranty claims were filed within 180 days of purchase — indicating possible early defects.  
**Recommendation:** Strengthen quality control checks before shipment.

---

### 3. Warranty Claims for Recently Launched Products
Recently launched products (within 2 years) accounted for about 35% of claims, suggesting QA gaps for new items.  
**Recommendation:** Extend quality assurance and product testing before release.

---

### 4. High-Sales Months in the USA
Sales exceeded 5,000 units during **November, December, and April**, aligning with holidays and launch events.  
**Recommendation:** Prepare additional stock and promotional campaigns during these peak months.

---

### 5. Product Category with Most Warranty Claims
The **Wearables** category (Apple Watch, AirPods) had the highest claim rate.  
**Recommendation:** Improve design durability and enhance after-sales services.

---

## Insights and Recommendations

| Area | Insight | Recommendation |
|------|----------|----------------|
| Product Portfolio | Older accessories have weak sales | Discontinue or reposition these products |
| Quality Control | Early warranty claims are high | Strengthen pre-launch testing |
| Launch Strategy | New products show above-average claim rates | Implement extended testing cycles |
| Sales Planning | Clear seasonal peaks in USA | Align stock and campaigns with sales cycles |
| After-Sales Service | Wearables have high claim volume | Improve repair service and customer experience |


