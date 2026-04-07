**Readme of Hands on L11** 

[Cloudwatch Screenshot](photos/cloudwatch-crawler.png)

**Query 1 Screenshot**
![Query 1 Screenshot](photos/query1.png)
SQL Code Created below
```
SELECT * FROM "output_db"."raw" limit 10;
```
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