# LITA_Capstone_Project

[Project Overview](#project-overview)

[Project Title](#project-title)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Explorative Data Analysis](#explorative-data-analysis)



## Project Overview

As a student of Data Analysis tutored by the Incubator HUB, I carried out my project by exploring and implementing tools used during our classes for this project, showing my analytic skills and performance.
 
### Project Title:  
#### Sales Data

### Data Sources
- Open Source ; LMS
- Excel csv

### Data Cleaning and Preparations
```
The following action was performed in the initial stage of Data Cleaning;
1. Data loading and Inspection
2. Handling missing variables
3. Data Cleaning and formatting.
```

#### Tools Used 
- Microsoft Excel
- SQL - Structured Query Language
- Power BI

### Sales Data

- Microsoft Excel [Download Here](http://www.microsoft.com

  1. This entails data collected from Customers at different regions durimg a specific period of time, analyzing the performance of sales of a retail store. 
  2. Data cleaning
  3. Data Visualization


### Explorative Data Analysis

#### Excel

```
This involved exploring of the Data to answer some questions about the Data such as;
- Total Revenue By Region
- Total Sales Of Product By Region
- Total Sales of peoduct Per Month
- Total Sales Of Product By Transaction Category
- Quantity Of Product Sold By Region Per Year
- Total Sales of Product Per Year
- Percentage Quantity of Product Sold By Region
```
SQL For Sales Data
```
- Total sales for each product category.
- Number of sales transactions in each region.
- Highest-selling product by total sales value.
- Monthly sales totals for the current year.
- Top 5 customers by total purchase amount.
- Percentage of total sales contributed by each region.
- Products with no sales in the last quarter.
- Average Sales Of Product
```
SQL For Customer Data
```
- Total number of customers from each region.
- Most popular subscription type by the number of customers.
- Customers who canceled their subscription within 6 months.
- Average subscription duration for all customers.
- Customers with subscriptions longer than 12 months.
- Total revenue by subscription type.
- Top 3 regions by subscription cancellations.
- Total number of active and canceled subscriptions.
```


### SQL
   ```SQL
   SELECT *FROM TABLE [dbo].[LITA Capstone Project Dataset]
   GROUP BY Region
   ```

``` SQL
Retrieve the total sales for each product category
SELECT *PRODUCT, SUM(Quantity) as Total_Sales
From [dbo].[Sales Data Sql]
GROUP BY Product;
```
```SQL
Number of sales Transaction per region
Select Region, COUNT(*) as Total_transaction
From [dbo].[Sales Data Sql]
Group By Region;
```
```SQL  
Highest Selling Product By Total Sales
Select top 1 PRODUCT, SUM(Quantity) As Sales_Unitprice
From [dbo].[Sales Data Sql]
Group by Product;
```
```SQL
Total Revenue Per Product
Select PRODUCT, SUM(Quantity*UnitPrice) as TotalSales 
From [dbo].[Sales Data Sql]
Group By Product;
```
```SQL
Total Monthly Sales For The current Year
Select MONTH(OrderDate) As Month, 
sum(Quantity *UnitPrice) As Monthly_Sales
From [dbo].[Sales Data Sql]
Where YEAR(orderDate)=  YEAR(GetDate())
Group by MONTH(Orderdate)
Order By Month;
```
```SQL
Top 5 Customers by Total Purchase Amount
Select Top 5 Customer_id, sum(Quantity *Unitprice) as TotalPurchaseAmount
From[dbo].[Sales Data Sql]
Group By Customer_Id
Order By TotalPurchaseAmount Desc;
```
```SQL
Percentage of Total sales contributed by each region
Select Region, 
SUM(Quantity * Unitprice) As TotalSales,
SUM(Quantity * Unitprice) * 1.0/ (Select SUM(Quantity * UnitPrice)
From [dbo].[Sales Data Sql])* 100
As PercentageofTotalSales
From [dbo].[Sales Data Sql]
Group By Region
```
```SQL
Product with No Sales In The Last Quarter
Select Distinct PRODUCT, OrderID, Quantity
From [dbo].[Sales Data Sql]
Where Product NOT IN
Select Distinct PRODUCT
From [dbo].[Sales Data Sql]
Where OrderDate Between '2024-06-01' AND '2024-09-30'
```
#### Data Visualization 



### Customer Data
#### Excel


SQL
```SQL
Select *From [dbo].[Customer Data];
```
```SQL
Retrieve Total Number Of Customers From Each Region
Select Region,
Count(Distinct CustomerId)
As Total_Customers
From [dbo].[Customer Data]
Group By Region;
```
```SQL
Most Popular Subscription Type By Number of Customers
Select Top 1 Subscriptiontype,
Count(Distinct Customerid) As Total_Customers
from [dbo].[Customer Data]
Group By SubscriptionType
Order By Total_Customers Desc;
```
```SQL
Customers Who Cancelled Their Subscription Within 6 months------
Select customerId
From [dbo].[Customer Data]
Where Datediff(Month, SubscriptionStart, SubscriptionEnd) <= 6;
```
```SQL
Average Subscription Duration for All Customers
Select Avg(Datediff(Day,SubscriptionStart, SubscriptionEnd))
As Avg_Subscription_Duration
From [dbo].[Customer Data]
```
```SQL
Customer With Subscription Longer Than 12 Months
Select CustomerId
From [dbo].[Customer Data]
Where DATEDIFF(Month,SubscriptionStart, SubscriptionEnd) > 12;
```
```SQL
Total Revenue By Subscription Type
Select SubscriptionType,
Sum(Revenue) As Total_Revenue
From [dbo].[Customer Data]
Group By SubscriptionType;
```
```SQL
Top 3 Regions By Subscription Cancellation
Select Top 3 Region,
Count(*) As SubscriptionEnd_Count
From [dbo].[Customer Data]
Where SubscriptionEnd is null
Group By Region
Order By SubscriptionEnd_Count Desc
```
```SQL
Total Number Of Active & Cancelled Subscription
Select S(CASE WHEN SubscriptionEnd IS NULL THEN 1 As  Active_Subscription,
Sum(CASE WHEN SubscriptionEnd IS NOT NULL THEN 1 ElSE 0 END) As Cancelled_Subscription
From [dbo].[Customer Data]
```

