# sql1
1.	to find total liquor sales in IOWA
SELECT SUM(sale_dollars)
  
<img width="323" alt="image" src="https://user-images.githubusercontent.com/100938096/156758972-96f2cf58-8944-4a16-8487-c65d00dbf34a.png">


FROM `bigquery-public-data.iowa_liquor_sales.sales` 

 

2.	TO FIND MAXIMUM PACKS SOLD OF A SINGLE LIQUOR BRAND

SELECT item_description, MAX(pack) AS Pack
FROM `bigquery-public-data.iowa_liquor_sales.sales` 
GROUP BY item_description
ORDER BY Pack DESC limit 5

 <img width="369" alt="image" src="https://user-images.githubusercontent.com/100938096/156759010-fd70fb88-1007-4b64-92f1-6dc826078fa3.png">


3.	What is the most popular consumed liquor in Iowa?
SELECT 
item_description
,ROUND(SUM(volume_sold_gallons),2) AS gallons_sold
FROM `bigquery-public-data.iowa_liquor_sales.sales` 
GROUP BY 1
ORDER BY 2 DESC limit 5
 
<img width="318" alt="image" src="https://user-images.githubusercontent.com/100938096/156759036-e3442978-0eb0-469b-8cb1-f5ee87f20521.png">


4.	What stores have sold the most gallons of liquor?
SELECT
store_name,
store_location,
ROUND(SUM(volume_sold_gallons),2) AS gallons_sold
FROM
`bigquery-public-data.iowa_liquor_sales.sales`
GROUP BY
store_name,
store_location
ORDER BY
gallons_sold DESC limit 5

 <img width="335" alt="image" src="https://user-images.githubusercontent.com/100938096/156759064-30a042a0-c57a-4201-854e-c30ae676b669.png">


5.	numbers of bottles sold in distinct city

SELECT DISTINCT city, COUNT(bottles_sold) AS bottles 
FROM `bigquery-public-data.iowa_liquor_sales.sales` 
GROUP BY city, bottles_sold limit 5
 
<img width="280" alt="image" src="https://user-images.githubusercontent.com/100938096/156759087-6d74bcc9-8942-43a7-a93f-a614407b4256.png">

6.	total number of stores 
SELECT COUNT(distinct store_name) 
 FROM `bigquery-public-data.iowa_liquor_sales.sales` 
 <img width="205" alt="image" src="https://user-images.githubusercontent.com/100938096/156759119-d06667a2-4731-4630-9780-5d640628ef25.png">


7.	number of stores of HY-Vee brand
SELECT COUNT(distinct store_name) 
  FROM `bigquery-public-data.iowa_liquor_sales.sales` 
WHERE store_name LIKE '%Hy-Vee%'
 
<img width="198" alt="image" src="https://user-images.githubusercontent.com/100938096/156759146-8afe8510-6261-4917-a0b4-7a5d11eccc93.png">

8.	stores that have the same number of sales as the previous year
SELECT st.store_name,st.sale_dollars
FROM `bigquery-public-data.iowa_liquor_sales_forecasting.2020_sales_train` st
INNER JOIN `bigquery-public-data.iowa_liquor_sales_forecasting.2021_sales_predict` sp ON
st.sale_dollars=sp.sale_dollars
GROUP BY st.store_name, st.sale_dollars limit 5
 
<img width="325" alt="image" src="https://user-images.githubusercontent.com/100938096/156759177-d567f89b-be45-4f6f-8e2c-ae17f77667c8.png">

9.	average sales of Hy-Vee store in the year 2021

SELECT avg(y.sale_dollars) as sale_dollars_2020,avg (x.sale_dollars) as sale_dollars_2021
from 
bigquery-public-data.iowa_liquor_sales_forecasting.2021_sales_predict x
full outer join bigquery-public-data.iowa_liquor_sales_forecasting.2020_sales_train y 
on x.store_name = y.store_name
where y.store_name LIKE '%Hy-Vee%'

 <img width="350" alt="image" src="https://user-images.githubusercontent.com/100938096/156759215-cbf95d16-5659-43a3-a10f-e7ee1bcc4b53.png">


10.	average sales of Fareway Stores store in the year 2021
SELECT avg(y.sale_dollars) as sale_dollars_2020,avg (x.sale_dollars) as sale_dollars_2021
from 
bigquery-public-data.iowa_liquor_sales_forecasting.2021_sales_predict x
full outer join bigquery-public-data.iowa_liquor_sales_forecasting.2020_sales_train y 
on x.store_name = y.store_name
where y.store_name LIKE '%Fareway Stores%'

<img width="330" alt="image" src="https://user-images.githubusercontent.com/100938096/156759235-33a62b59-4037-4dee-833e-b8339ed7a9c3.png">




 


