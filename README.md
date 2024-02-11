# Brazilian E-Commerce Public Dataset by Olist

## Introduction
**Welcome to the AI Variant Data Analyst Internship Project:** 
- Olist is an E- commerce company  is a Brazilian department store platform which operates in the e-commerce segment (Software as Service). 
- The service consists of management of the sales process between shopkeepers and clients and includes a client satisfaction report.
- The advantages for the shopkeepers is a better market presence and transparent reputation metrics and sells the products to customer directly through Olist’s store  logistics. 

## Project Overview
- **Domain:** E-Commerce Sales Analytics
- **Project Name:** Brazilian-E-Commerce Sales
- **Dataset Names:**
  1. Olist_E-commerce_dataset
  2. olist_customers_dataset
  3. olist_geolocation_dataset
  4. olist_order_items_dataset
  5. olist_order_payments_dataset
  6. olist_order_reviews_dataset
  7. olist_orders_dataset
  8. olist_products_dataset
  9. olist_sellers_dataset
- **Dataset Type:** Excel cvs Data
- **Dataset Size:** 1,00,000 records each

## Key Performance Indicators (KPIs)
The project emphasizes five key performance indicators (KPIs) to gain insights into employee retention and related factors:

1. Weekday Vs Weekend (order_purchase_timestamp) Payment Statistics
2. Number of Orders with review score 5 and payment type as credit card.
3. Average number of days taken for order_delivered_customer_date for pet_shop.
4. Average price and payment values from customers of sao paulo city.
5. Relationship between shipping days (order_delivered_customer_date - order_purchase_timestamp) Vs review scores.

## Tools used for Visulize
- **Excel**
- **Power BI**
- **Tableau**
- **MySql**

## A Roadmap to Effective Analysis
- Define the Question 		
- Collect & import the data 
- Clean the data by data modeling
- Analyze the data
- Visualize reports	& share insights

## Dashboard Creation
### Architecture of Data Schema
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/62010370-e417-4c05-ad7d-16695c26c6ce)
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/2157d6dc-2d12-4c23-af65-653b3a124c27)

### Excel Dashboard
The Excel dashboard provides a clear and organized platform for visualizing critical E-Commerce Sales Analytics insights. It utilizes various data visualization components such as charts, graphs, and PivotTables to represent key performance indicators (KPIs) effectively. User-friendly features like dropdown menus, data filtering, and dynamic updates enhance the user experience.
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/6c30a705-bbb3-4811-b6ea-c3be539f7104)

### Power BI Dashboard
The Power BI dashboard offers an immersive and interactive data exploration experience, allowing users to uncover insights and trends within the E-Commerce Sales dataset. Its intuitive layout balances visualizations and filtering options, ensuring clarity and responsiveness. Here are some key features of the Power BI dashboard:
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/0467f399-ecb5-449e-901b-32974844e678)
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/e8e28220-e8fe-493b-a430-17372d107733)
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/f20fab5d-da0e-448b-a4c3-37ba351b0942)
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/33e743d1-4831-4cd8-827e-a0f88fe1879a)


### Tableau Dashboard
The Tableau dashboard provides an interactive platform for in-depth E-Commerce Sales Analytics, facilitating a deeper understanding of Brazilian-E-Commerce Sales patterns. Its modern design integrates a variety of data visualization components, including bar charts, donut charts, and more, to depict KPIs. Here are some highlights of the Tableau dashboard:
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/1c153637-6db1-4af1-897c-51574ef2b82a)
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/fb5e6a01-2852-4f08-9572-a29a6464dc2e)


## MySQL
The E-Commerce Sales dataset was imported into an SQL database. An E-Commerce Sales database is a system where you store and manage data on your company's sales transactions. E-Commerce databases can be used to track a variety of information, including sales metrics, which give the sales team insights for better decision-making..

### KPI 1: Weekday Vs Weekend (order_purchase_timestamp) Payment Statistics.
    SELECT
        CASE WHEN DAYOFWEEK(od.order_purchase_timestamp) IN (1, 7) THEN 'Weekend' ELSE 'Weekday' END AS "Day Type",
        round(sum(opd.payment_value)) AS "Average Payment Amount"
    FROM
        olist_orders_dataset od
        JOIN olist_order_payments_dataset opd ON od.order_id = opd.order_id
    GROUP BY
        CASE WHEN DAYOFWEEK(od.order_purchase_timestamp) IN (1, 7) THEN 'Weekend' ELSE 'Weekday' END;
        
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/ccf3a725-2ae6-4aa7-9159-24b88ebd5c4b)


### KPI 2: Number of Orders with review score 5 and payment type as credit card.
    SELECT
        count(od.order_id) AS "Number of Orders",ord.review_score,opd.payment_type
    FROM
        olist_orders_dataset od
    	JOIN olist_order_payments_dataset opd ON od.order_id = opd.order_id
        JOIN olist_order_reviews_dataset ord ON opd.order_id = ord.order_id
    WHERE
        opd.payment_type = 'credit_card'
        AND ord.review_score = 5;
  ![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/6e83b78d-3797-4740-a72e-58943abe5c26)


### KPI 3: Average number of days taken for order_delivered_customer_date for pet_shop.
    SELECT
        round(AVG(od.order_delivered_customer_date)) AS "Average Delivery Time (Days)",op.product_category_name
    FROM
        olist_orders_dataset od
        JOIN olist_order_items_dataset oi ON od.order_id = oi.order_id
        JOIN olist_products_dataset op ON oi.product_id = op.product_id
    WHERE
        op.product_category_name = 'pet_shop'
        AND od.order_delivered_customer_date IS NOT NULL
        group by op.product_category_name;
![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/e1506165-b093-4a00-af93-c52fca987796)


### KPI 4: Average price and payment values from customers of sao paulo city.
    SELECT
        round(AVG(oi.price)) AS "Average Order Price",
        round(AVG(op.payment_value)) AS "Average Payment Value"
    FROM
        olist_orders_dataset od
        JOIN olist_order_items_dataset oi ON od.order_id = oi.order_id
        JOIN olist_order_payments_dataset op ON od.order_id = op.order_id
        JOIN customers_dataset c ON od.customer_id = c.customer_id
        JOIN olist_geolocation_dataset og ON c.customer_zip_code_prefix = og.geolocation_zip_code_prefix
    WHERE
        c.customer_city = 'Sao Paulo';
  ![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/a3396f84-dff3-44b8-8cc1-5785d5b389b4)

### KPI 5: Relationship between shipping days (order_delivered_customer_date - order_purchase_timestamp) Vs review scores.
        SELECT
        ord.review_score,
        round(AVG((od.order_delivered_customer_date))) AS "Average Shipping Days"
    FROM
        olist_orders_dataset od
        JOIN olist_order_reviews_dataset ord ON od.order_id = ord.order_id
    WHERE
        od.order_delivered_customer_date IS NOT NULL
        AND od.order_purchase_timestamp IS NOT NULL
    GROUP BY
        ord.review_score;
  ![image](https://github.com/Harmanprits/Brazilian-E-Commerce-Public-Dataset-by-Olist/assets/142983120/34522be1-9c46-4aff-883c-f13f772fac7c)

## Conclusion and Recommendations
- **Offers and Discounts** must provide on  weekends to balances the weekdays payments .
- On Mondays,**New Products** must launch as payments count is more.
- **11,974 orders** have Review score **“1”** may be due to lack of **quality or delay** in delivery of item.
- By **reducing Shipping days**,the fast delivery of order will be **increase**.
- Olist must focus on **product quality** which has review score “ 1 ”.
- Olist must enhance delivery procedure by increasing warehouses for various product and  has to **recruit more staff to decrease shipping time**.
- Olist must focus on purchase and  delivery process in Sao Paulo city and must **improve transactions in other cities also**.
- Delivery time must improve by Olist – logistics service.
- **Minimizing the shipping days would lead to more positive reviews**. Consecutively customer satisfaction will be met which leads to more business.
- High quality products must supply of better review score and to **conclude the low review score**.

