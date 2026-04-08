# Readme of Hands on L11

**Cloudwatch Screenshot located below**
![Cloudwatch Screenshot](photos/cloudwatch-crawler.png)

**Query 1 Screenshot**
![Query 1 Screenshot](photos/query1.png)
SQL Code created below
```
SELECT * FROM "output_db"."raw" limit 10;
```
<br>

**Query 2 Screenshot**
![Query 2 Screenshot](photos/query2.png)
SQL Code created below
```
SELECT distinct(category), 
count("category")
FROM "output_db"."raw"
GROUP BY 
category
limit 10;
```
<br>

**Query 3 Screenshot***
![Query 3 Screenshot](photos/query3.png)

SQL Code Created below
```
SELECT distinct(fulfilment),
count("order id") as "Number of Orders", 
sum("qty") as "Items sold", 
sum("amount") as "Revenue"
FROM "output_db"."raw"
WHERE "status" != 'Cancelled' and "order id" != 'Pending'
GROUP by
fulfilment
Order by "Revenue" DESC
limit 10;
```
<br>

**Query 4 Screenshot**
![Query 4 Screenshot](photos/query4.png)

SQL Code created below
```
SELECT SUBSTRING("date", 1, 2) as month,
count("order id") as "Number of Orders",
sum("amount") as "Revenue"
FROM "output_db"."raw" 
WHERE "status" != 'Cancelled' and "order id" != 'Pending'
GROUP by SUBSTRING("date", 1, 2)
Order by month ASC
limit 10;
```
<br>

**Query 5**

**Screenshot for Query 5 



```
SELECT category, sku, "Number of Orders", "Total Revenue"
FROM (
    SELECT 
        category, 
        sku, 
        COUNT("order id") AS "Number of Orders",
        SUM("amount") AS "Total Revenue",
        ROW_NUMBER() OVER (
            PARTITION BY category 
            ORDER BY SUM("amount") DESC
        ) AS rn
    FROM "output_db"."raw"
    WHERE "status" != 'Cancelled' 
      AND "status" != 'Pending' 
      AND qty >= 1
    GROUP BY sku, category
) ranked_skus
WHERE rn <= 5
ORDER BY "Total Revenue" DESC;
```