# Readme of Hands on L11

**Cloudwatch Screenshot located below**
[Cloudwatch Screenshot](photos/cloudwatch-crawler.png)

**Query 1 Screenshot**
![Query 1 Screenshot](photos/query1.png)
SQL Code Created below
```
SELECT * FROM "output_db"."raw" limit 10;
```
<br>

**Query 2 Screenshot**
![Query 2 Screenshot](photos/query2.png)
SQL Code Created below
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


