# Data-Warehouse-Project
## Project Summary:
The primary objective of this project is to create a concept data warehouse using dimensional modelling techniques. Identify the key stakeholders and business requirements for the same. Based on these requirements develop a design schema for the data warehouse. Create the warehouse using any ETL tools. Produce reports in support of the requirements using SSRS and R. Develop an XML schema based on the data warehouse. Implement a part of the data warehouse as graph database using Neo4j technologies.

## Source and background:
The data source that I have used for this project is Northwind.

The Northwind database is a fictional B2B ( Business to Business) trading company that imports and exports specialty food items. It includes data consisting of product information, orders, order details, customer, employee and a few more.
This is one of the most dynamic database as it can be applied to a variety of applications which is why I was very keen on working with this data set.
There is a wide variety of dimensions that can be created for a number of analysis.
Using this source I have created a data warehouse called NW_Trading_DW.
This warehouse is created to maintain optimal ratio of stock to WIP ( Work In Progress) based on their reorder level and ordered quantities. The idea is to ensure customer satisfaction with timely product delivery. 
It also helps keep a track of premium customers, most selling products, supply chain management (SCM) and employee performance.
The key stakeholders include the Employees, Customers and Suppliers.

## Business Requirements:
1.	Implement J.I.T.(Just in time): A Japanese model to manage deliveries. 
2.	Customer retention.
3.	Employee incentive Program.
4.	Optimize supply chain management.
5.	Optimize delivery time.

## Design schema for the data warehouse:
![schema](https://user-images.githubusercontent.com/46936497/61000136-a4dc6b80-a354-11e9-9ff2-ae97a9c6ac38.png)

A Constellation/ Galaxy of stars in data warehouse modelling is a dimensional model having multiple facts. I have used this model to create a star schema with two fact tables. The dimensions and facts and their relations are displayed in the above schema that I have created using Lucid chart. 
### Dimensions: 
The information obtained from the dimension table is used to do the analysis. The dimension tables contain descriptive and numeric values. Each dimension  table has a unique Primary Key which is then used to create the linking relation with the fact tables.For the NW_Trading_DW the dimensions that I have created are Customer, Employee, Supplier which are also my key stakeholders. These contain various attributes that provide further information about the stake holders. These attributes are mentioned above and are  self-explanatory. The other dimensions are : 
Product, which are being traded by Northwind, 
Category, categories information in which the products are divided into,
Calendar, which gives the date and time specific information of sales. It also gives a quarterly/ monthly or annual details. 
### Fact Tables: 
The fact tables usually contain numeric measures of the subject of analysis. I have created two aggregate fact tables:
### 1.	CustomerEmployee_Fact:
This fact table takes the Employee details from the Employee_Dim using EmployeeKey as foreign key , Similarly, Customer details from the Customer_Dim using  CustomerKey as foreign key and date and time specific details from the Calendar_Dim using CalendarKey as foreign key. This tables takes the dynamic value of Order Id from the source database Northwind. Together with the order id and the other three dimensions I have created an attribute of Sales that determines the total sales by each customer and the sales under each employee. This fact table can be used to determine the premium customers and best employees. Thus fulfilling the business requirements 2 and 3.This tables can be used to do specific time related analysis. Also, we can determine region specific sales and many other analysis few of which are displayed in the upcoming sections.

### 2.	ProductInStock_Fact:
This fact is used to keep a track of the units in stock and the units on order of each product based on its reorder level. This is done to maintain the correct balance of the products stocked to their orders. It helps implement the business requirement 1 mention in section 2.1.This fact takes the order details from the source database Northwind using the attribute orderid. It also takes the Product details from the Product_Dim using the productKey as foreign key. The category details from Categories_Dim using CategoriesKey as foreign key and date and time specific information from the Calendar_Dim similar to the CustomerEmployee_Fact. This fact table also takes the Supplier information from the Supplier_Dim the SupplierKey as Foreign key. This fact can be used to perform multiple analysis like the most selling product in each category and a few more mentioned in further sections. This fact helps fulfil requirement 4 and 5 from the business requirements section.

## Implementing In SQL:
To implement the Data Warehouse I have used SQL statements to create and insert values. Code attached.

## Visualizations and R Code:

### Units on Orders v/s Units in Stock(Category: Beverage) :
This graph not only helps ensure the products are sufficiently stocked for timely deliveries but also helps the company take business decisions on overly stocked products. Tom improve the sales of such slow moving products the company can decide on discounts or offers on such products. To implement the J.I.T model, the company can further analyze as to why these products are overly stocked and create a better plan for product stocking. This in turn will reduce the warehousing cost and space.
![v1](https://user-images.githubusercontent.com/46936497/61000538-917dd000-a355-11e9-8cf3-066a1b807310.png)

### 2.	Shipping more than a week: 
This graph helps in analyzing the delivery times of shipment in different countries. It targets the countries that take more than a week to deliver to. The company can further investigate as to why the delivery times are higher compared to other countries and come up with relevant action plans. The customers can be offered higher discounts or special deals to compensate for the prolonged delivery times. There can be a common stock yard planned for certain cluster of countries based on their geographic locations to reduce the delivery times.


