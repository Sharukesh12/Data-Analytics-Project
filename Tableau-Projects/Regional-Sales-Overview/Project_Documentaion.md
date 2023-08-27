# Regional Sales Overview

![image](https://assets.website-files.com/60e7f71b22c6d0b9cf329ceb/621e193892e8c41051e34fce_StepsforEffectivelyAnalyzingYourSalesData_20971e108bda1d8795a0c640c000e691_2000.png)

### Problem Statement:
Atliq Hardware, a prominent manufacturer of computer hardware and peripherals, operates nationwide with a presence in Surge Stores, Nomad Stores, Excel Stores, and Electricalsara Stores, supplying them with various hardware equipment. The company's headquarters is located in Delhi, and it maintains regional district offices across India. Heading the sales department is Bhavin Patel, the Sales Director of Atliq Hardware.

Bhavin Patel currently confronts a significant challenge: despite its widespread operations, the company has been experiencing a decline in sales. Identifying the underlying cause of this decline has proven elusive for him. In response, Bhavin Patel has taken the step of enlisting the assistance of a data analyst. 

The primary objective is to extract valuable insights that can shed light on the reasons behind the decline in sales. These insights will serve as a foundation for refining the company's business strategies.

The specific insights that Bhavin Patel seeks to uncover through data analysis are as follows:
1. **Regional Sales Breakdown:** The data analysis will provide a breakdown of sales across different regions, including Central, North, and South.
2. **Daily Sales:** The data analysis will provide a line chart for last 2 weeks, offering a snapshot of sales performance on a daily basis per region.
3. **Top Sales-Generating Cities:** The analysis will identify and visualize the cities per rigion that contribute the most to the company's sales figures.
4. **Year-on-Year Profit and Sales Comparison:** A comparison of profit and sales figures from the current year with previous year will be presented, highlighting changes in percentage(%).
5. **Order Details:** Detailed information about customer orders will be provided, offering insights into profit or loss value for each product sold.

### Purpose:
By leveraging the capabilities of the hired data analyst, Bhavin Patel aims to unravel the complexities behind the sales decline and pave the way for data-informed strategies that can lead to a resurgence in the company's sales performance. Simultaneously, the intention is to streamline and automate these insights to minimize the manual effort and time currently invested in data collection processes.

### Stakeholders:
- Sales Director
- Marketing Team
- Customer Service Team
- Data & Analytics Team
- Information Technology (IT) Department

### Actions Taken in the Project:

**In PostgreSQL:**
1. Created a new database named 'sales_db'.
2. Successfully downloaded and restored the ‘sales_dump.sql’ file into the ‘sales_db’ database.
3. Conducted data analysis using SQL with following queries:

    - Displayed all customer records.
        ```sql
        SELECT * FROM customers;
        ```
    - Counted the total number of customers.
        ```sql
        SELECT COUNT(*) AS total_customers 
        FROM customers;
        ```
    - Displayed transactions for the Chennai market (market code 'Mark001').
        ```sql
        SELECT * 
        FROM transactions 
        WHERE market_code='Mark001';
        ```
    - Listed distinct product codes of items sold in the Chennai market.
        ```sql
        SELECT DISTINCT(product_code) 
        FROM transactions 
        WHERE market_code='Mark001';
        ```
    - Displayed transactions where the currency is US dollars.
        ```sql
        SELECT * 
        FROM transactions 
        WHERE currency="USD";
        ```
    - Combined the ‘transactions’ and ‘date’ tables based on the order date, displaying transactions for the year 2020
        ```sql
        SELECT * 
        FROM transactions INNER JOIN date ON transactions.order_date = date.date 
        WHERE year = 2020;
        ```
    - Calculated the total revenue for the year 2020 by summing up sales amounts from transactions.
        ```sql
        SELECT SUM(transactions.sales_amount) 
        FROM transactions INNER JOIN date ON transactions.order_date=date.date 
        where date.year=2020;
        ```
    - Calculated the total revenue for January 2020 by summing up sales amounts from transactions
        ```sql
        SELECT SUM(transactions.sales_amount) 
        FROM transactions 
        INNER JOIN date ON transactions.order_date=date.date 
        WHERE date.year=2020 and date.month_name="January";
        ```
    - Calculated the total revenue for the year 2020 specifically for the Chennai market.
        ```sql
        SELECT SUM(transactions.sales_amount)
        FROM transactions 
        INNER JOIN date ON transactions.order_date=date.date 
        WHERE date.year=2020 and transactions.market_code="Mark001";
        ```

By executing these SQL queries, valuable insights have been extracted from the data, contributing to a deeper understanding of various sales-related aspects.

**In Tableau:**

1. Imported tables from PostgreSQL as CSV files in Tableau Public.
2. Created a Star Schema by joining tables, with 'Transactions' as the fact table and other tables as dimension tables.
3. Performed data cleaning:
    - Removed markets 'Mark097' and 'Mark999' as they don't apply to India.
    - Normalized sales amount by converting USD to INR using a calculated field.

**Dashboard Creation in Tableau:**
1. Created calculated fields for various indicators, profit, sales, and order changes, and their respective percentage changes.
2. Utilized Level of Detail (LOD) expressions to calculate indicators based on the current and prior years.
3. Built a dashboard using the calculated fields to display various insights.
[![Regional Sales Overview](URL_TO_YOUR_IMAGE)](https://public.tableau.com/views/SalesOverview_16930746847990/RegionalSalesOverview?:language=en-US&:display_count=n&:origin=viz_share_link)