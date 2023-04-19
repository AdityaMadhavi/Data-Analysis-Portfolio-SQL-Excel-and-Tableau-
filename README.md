# Data-Analysis-Portfolio-SQL-Excel-and-Tableau-
Applied SQL queries to get the appropriate data using join and aggregate functions. 
2) Then connected my SQL database with Excel using the SQL query and performed further data analysis.
3) Connected my Excel with Tableau to visulaize the data. 
**SQL Code**
use BikeStores;
SELECT ord.order_id,
	concat(cust.first_name,'-',cust.last_name) as 'customers',
	cust.city,
	cust.state,
	ord.order_date,
	SUM(ite.quantity) AS 'total_units',
	SUM(ite.quantity* ite.list_price) AS 'revenue', 
	pro.product_name, 
	cat.category_name,
	sto.store_name,
	CONCAT(sta.first_name,'-',sta.last_name) AS 'Sales_rep',
	bra.brand_name 
FROM sales.orders ord
JOIN sales.customers cust
ON ord.customer_id=cust.customer_id
JOIN sales.order_items Ite
ON ord.order_id= ite.order_id
JOIN production.products pro
ON ite.product_id = pro.product_id
JOIN production.categories cat
on pro.category_id = cat.category_id
JOIN sales.stores sto
ON ord.store_id =sto.store_id
JOIN sales.staffs sta
ON ord.staff_id =sta.staff_id


JOIN  production.brands bra
ON pro.brand_id =bra.brand_id

GROUP BY  ord.order_id, concat(cust.first_name,'-',cust.last_name), cust.city, cust.state, ord.order_date,pro.product_name,cat.category_name,sto.store_name,CONCAT(sta.first_name,'-',sta.last_name),bra.brand_name 
