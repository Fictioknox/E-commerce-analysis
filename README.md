# E-Commerce Sales Analysis Report

## Overview

This project analyzes transactional data from a UK-based online retailer using the [Online Retail Dataset](https://www.kaggle.com/datasets/vijayuv/onlineretail) from Kaggle, licensed under CC0-1.0. The dataset contains ~540,000 records of sales transactions (invoices, products, quantities, prices, customer IDs, and dates) from 2010–2011. The goal was to extract actionable business insights using SQL, demonstrating proficiency in data manipulation, aggregation, and advanced querying techniques.

The analysis was performed in Google Colab using SQLite, with a 20,000-row sample to ensure efficient processing. Six SQL queries were executed to uncover insights into customer behavior, product performance, and market trends, supporting strategic decision-making for the retailer.

## Dataset Description

The dataset includes the following key fields:
- **InvoiceNo**: Unique identifier for each transaction.
- **StockCode**: Product code.
- **Description**: Product name.
- **Quantity**: Number of units sold or returned.
- **InvoiceDate**: Transaction date and time.
- **UnitPrice**: Price per unit.
- **CustomerID**: Unique customer identifier.
- **Country**: Customer’s country.

A SQLite table (`Retail`) was created to store this data, and a 20,000-row random sample was used to balance performance and insight depth.

## Analysis and Insights

The project executed six SQL queries, each addressing a specific business question. Below are the queries, their results (based on the provided output), and the insights derived.

### Query 1: Total Revenue by Country

**Objective**: Identify the top revenue-generating markets.

**SQL Techniques**: `SUM`, `ROUND`, `GROUP BY`, `ORDER BY`, `WHERE`.

**Results**:
```
          Country  total_revenue
0  United Kingdom      242094.80
1     Netherlands       11394.20
2            EIRE       11061.86
3         Germany        8170.93
4          France        7198.34
```

**Insights**:
- The United Kingdom dominates with $242,094.80 in revenue, reflecting the retailer’s primary market.
- Netherlands and EIRE contribute significantly ($11,394.20 and $11,061.86), indicating strong European demand.
- Germany and France are smaller but notable markets, suggesting potential for targeted expansion.

**Business Implication**: Focus marketing efforts on the UK while exploring growth opportunities in Netherlands and EIRE through localized campaigns.

### Query 2: Top Products by Units Sold

**Objective**: Determine the best-selling products by units sold and revenue.

**SQL Techniques**: `SUM`, `ROUND`, `GROUP BY`, `ORDER BY`, `WHERE`.

**Results**:
```
                         Description  total_units_sold  total_revenue
0  WORLD WAR 2 GLIDERS ASSTD DESIGNS              5382        1083.54
1          ASSORTED COLOURS SILK FAN              2714        1842.30
2        GIN + TONIC DIET METAL SIGN              2351        4090.29
3            JUMBO BAG RED RETROSPOT              2345        4465.05
4    PACK OF 72 RETROSPOT CAKE CASES              2231        1134.75
```

**Insights**:
- “WORLD WAR 2 GLIDERS ASSTD DESIGNS” leads with 5,382 units sold, but its revenue ($1,083.54) is lower than others, indicating a low unit price.
- “JUMBO BAG RED RETROSPOT” and “GIN + TONIC DIET METAL SIGN” generate high revenue ($4,465.05 and $4,090.29), suggesting premium pricing or high demand.
- Products like “PACK OF 72 RETROSPOT CAKE CASES” appeal to bulk buyers, likely for events or resale.

**Business Implication**: Prioritize stocking high-revenue products like jumbo bags and metal signs, and consider bundling low-price items like gliders to boost sales.

### Query 3: High-Value Customers

**Objective**: Identify customers with above-average spending.

**SQL Techniques**: Common Table Expression (CTE), `SUM`, `ROUND`, subquery, `WHERE`, `GROUP BY`, `ORDER BY`.

**Results**:
```
   CustomerID  total_spent
0       14646     11109.03
1       17450      6413.94
2       14156      5475.62
3       14911      5457.88
4       18102      4909.15
```

**Insights**:
- Customer 14646 spends significantly more ($11,109.03) than others, marking them as a key account.
- Customers 17450, 14156, and 14911 also exceed the average spend, indicating a loyal, high-value segment.
- The top 5 customers contribute substantially to revenue, warranting personalized attention.

**Business Implication**: Implement loyalty programs or exclusive offers for these high-value customers to enhance retention and increase lifetime value.

### Query 4: Average Order Value by Country

**Objective**: Assess average order sizes across markets.

**SQL Techniques**: CTE, `SUM`, `ROUND`, `AVG`, `GROUP BY`, `ORDER BY`, `WHERE`.

**Results**:
```
       Country  avg_order_value
0  Netherlands           264.98
1    Australia           160.56
2       Sweden            96.33
3        Japan            95.03
4       Israel            86.35
```

**Insights**:
- Netherlands has the highest average order value ($264.98), suggesting customers place large or premium orders.
- Australia and Sweden follow with $160.56 and $96.33, indicating strong per-order spending in these markets.
- Japan and Israel have moderate order values, but their presence in the top 5 highlights untapped potential.

**Business Implication**: Target Netherlands and Australia with promotions for bulk purchases or high-value items to capitalize on their large order sizes.

### Query 5: Product Category Profitability

**Objective**: Analyze revenue by product categories derived from descriptions.

**SQL Techniques**: `CASE`, `COUNT DISTINCT`, `SUM`, `ROUND`, `GROUP BY`, `ORDER BY`, `WHERE`.

**Results**:
```
  product_category  unique_products  category_revenue
0            Other             2294         239060.28
1      Accessories              158          44084.29
2       Home Decor              126          21747.12
```

**Insights**:
- The “Other” category dominates with $239,060.28 in revenue across 2,294 unique products, indicating a broad range of uncategorized items.
- Accessories (e.g., bags, cases) contribute $44,084.29 with 158 products, showing strong demand for functional items.
- Home Decor (e.g., lights, lanterns) generates $21,747.12 with 126 products, appealing to aesthetic-driven buyers.

**Business Implication**: Refine product categorization to better understand the “Other” category, and increase inventory for Accessories and Home Decor to meet demand.

### Query 6: Top Repeat Customers

**Objective**: Identify customers with frequent purchases.

**SQL Techniques**: `COUNT DISTINCT`, `SUM`, `ROUND`, `GROUP BY`, `HAVING`, `ORDER BY`, `WHERE`.

**Results**:
```
   CustomerID  purchase_count  total_spent
0       14911             128      5457.88
1       17841             105      1504.47
2       12748              89      1376.68
3       15311              59      2503.84
4       14606              58       303.09
```

**Insights**:
- Customer 14911 is highly active with 128 purchases and $5,457.88 spent, indicating strong loyalty.
- Customers 17841 and 12748 have 105 and 89 purchases, respectively, but lower spend, suggesting frequent small orders.
- Customers 15311 and 14606 also show repeat behavior, with 59 and 58 purchases.

**Business Implication**: Engage these repeat customers with loyalty discounts or subscription models to maintain their frequent purchases.

## SQL Techniques Demonstrated

The project showcases a range of SQL skills:
- **Data Aggregation**: `SUM`, `COUNT`, `AVG` for revenue, units sold, and order values.
- **Filtering**: `WHERE` and `HAVING` to focus on relevant data (e.g., non-null CustomerIDs, multiple purchases).
- **Grouping**: `GROUP BY` for country, product, and customer-level analysis.
- **Subqueries and CTEs**: Used in Queries 3 and 4 to compute averages and order values.
- **Conditional Logic**: `CASE` in Query 5 to categorize products.
- **Sorting and Limiting**: `ORDER BY` and `LIMIT` to highlight top performers.
- **String Functions**: Implicit use in `LIKE` for categorization in Query 5.

## Conclusion

This E-Commerce Sales Analysis provides actionable insights for the online retailer:
- **Market Strategy**: Prioritize the UK, Netherlands, and EIRE, with targeted campaigns in high-order-value markets like Netherlands and Australia.
- **Product Management**: Focus on high-revenue products (e.g., jumbo bags) and expand Accessories and Home Decor inventory.
- **Customer Engagement**: Retain high-value and repeat customers (e.g., Customer 14646, 14911) through personalized offers and loyalty programs.

Future analyses could explore:
- Seasonal trends using full dataset date ranges.
- Detailed return analysis to identify quality issues.
- Customer segmentation by combining purchase frequency and spend.

This project demonstrates advanced SQL proficiency and delivers business value, making it a strong addition to a data analytics portfolio.
