Power BI DASHBOARD LINK(PIZZA SALES REPORT)

Dashboard - https://app.powerbi.com/groups/me/reports/9a81ef37-ada2-4b24-ae15-85d17178c88b/ReportSection5bb709e239119c4c1852?experience=power-bi

PROBLEM STATEMENT

This dashboard helps company understand sales on the basis of number of pizza sold ,best and worest pizza by quantity and size.

SQL Query steps followed :- Select * from dbo.pizza_sales

-- Total Revenue -- SELECT sum(total_price) as Total_Revenue from dbo.pizza_sales

-- Average order value per order it is nothing but total revenue by number of orders but in order no. we have no. of dulicates -- we will be taaking distinct values in order count to avoide duplicates -- Select sum(total_price)/count(distinct order_id) as Average_order_value from dbo.pizza_sales

-- Total Pizza Sold , it is sum total of all the quantities -- Select sum(quantity) as Total_pizza_sold from dbo.pizza_sales

-- Total Orders --

Select count(distinct order_id) As Total_Orders from dbo.pizza_sales

-- Average Pizza Per order -- Select cast(sum(quantity) AS decimal(10,2))/ cast(count(distinct order_id)AS decimal(10,2)) as Average_Pizza_Per_order from dbo.pizza_sales

-- Daily Trend for total orders --

Select DATENAME(DW,order_date) as order_day ,COUNT(distinct order_id) as Total_orders from dbo.pizza_sales Group by DATENAME(DW,order_date)

-- Monthly Trend for total orders --

Select DATENAME(MONTH,order_date) as Month_Name ,COUNT(distinct order_id) as Total_orders from dbo.pizza_sales Group by DATENAME(MONTH,order_date) order by Total_orders Desc

-- Percentage of sales by pizza Catagory-- select pizza_category ,sum(total_price) as total_sales,sum(total_price)*100/(select sum(total_price) from dbo.pizza_sales Where MONTH(order_date)=1) as PCT from dbo.pizza_sales Where MONTH(order_date)=1 Group by pizza_category

-- Percentage of sales by pizza size -- select pizza_size ,sum(total_price) as total_sales,sum(total_price)*100/(select sum(total_price) from dbo.pizza_sales ) as PCT from dbo.pizza_sales Group by pizza_size order by PCT

--Top 5 Best Sellers by Revenue , Total Quantity and Total Orders --

---------- Top 5 Pizza by Revenue ---------------------- Select TOP 5 pizza_name,sum(total_price) as Total_Revenue from dbo.pizza_sales Group by pizza_name Order by Total_Revenue Desc

---------- Bottom 5 Pizza by Revenue in this case we just convert all the data in ascending order to get botton 5 ---------------------- Select TOP 5 pizza_name,sum(total_price) as Total_Revenue from dbo.pizza_sales Group by pizza_name Order by Total_Revenue ASC

---------- Top 5 Pizza by Quantity ---------------------- Select TOP 5 pizza_name,sum(quantity) as Total_Quantity from dbo.pizza_sales Group by pizza_name Order by Total_Quantity DESC

---------- Bottom 5 Pizza by Quantity ---------------------- Select TOP 5 pizza_name,sum(quantity) as Total_Quantity from dbo.pizza_sales Group by pizza_name Order by Total_Quantity

---------- Top 5 Pizza by Orders ---------------------- Select TOP 5 pizza_name,Count(Distinct order_id)as Total_Orders from dbo.pizza_sales Group by pizza_name Order by Total_Orders DESC

---------- Top 5 Pizza by Orders ---------------------- Select TOP 5 pizza_name,Count(Distinct order_id)as Total_Orders from dbo.pizza_sales Group by pizza_name Order by Total_Orders

POWER BI DEX MEASURES

Average Order Value = [Total_Revenue]/[Total_orders]

Average Pizza Per order = [Total Pizzas Sold]/[Total_orders]

Order_Day = UPPER(LEFT(pizza_sales[Day_Name],3))

Order_Month = UPPER(LEFT(pizza_sales[Month Name],3))

Total Pizzas Sold = SUM(pizza_sales[quantity])

Total_orders = DISTINCTCOUNT(pizza_sales[order_id])

Total_Revenue = SUM(pizza_sales[total_price])
