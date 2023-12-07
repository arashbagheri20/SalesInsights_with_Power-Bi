# Project Objective
## Exploring AtliQ hardware sales data and creating a Power BI dashboard to understand the sales trends.
## Tools:
- Data Cleaning & Exploration: SQL Server
- Visualization: Power Bi
## 1	Data Cleaning & Exploration
### 	1.1	Download the `db_dump.sql` file to your local computer and import it
### 	1.2	Executing a query to Show all customer records
#### SQL Code Used:
	SELECT * FROM customers;
### 	1.3	Executing a query to Show the total number of customers
#### SQL Code Used:
	SELECT count(*) FROM customers;
### 	1.4	Executing a query to show transactions for Chennai market (market code for Chennai is Mark001
#### SQL Code Used:
	SELECT * FROM transactions where market_code='Mark001';
### 	1.5	Show distinct product codes that were sold in Chennai
#### SQL Code Used:
	SELECT distinct product_code FROM transactions where market_code='Mark001';
### 	1.6	Show transactions where the currency is US dollars
#### SQL Code Used:
	SELECT * from transactions where currency="USD"
### 	1.7	Show transactions in 2020 join by date table
#### SQL Code Used:
	SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;
###	 1.8	 Show total revenue in the year 2020,
#### SQL Code Used:
	SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";
### 	1.9 	Show total revenue in the year 2020, January Month,
#### SQL Code Used:
	SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");
### 	1.10	Show total revenue in the year 2020 in Chennai
#### SQL Code Used:
	SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
	and transactions.market_code="Mark001";
## 2	Power Bi Visualisation
### 	2.1	Formula to create norm_amount column
#### Dax Code Used:
`norm_amount column= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
