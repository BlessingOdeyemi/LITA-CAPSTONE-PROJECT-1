# LITA-CAPSTONE-PROJECT-1
This is where i document the process of answering the LITA Capstone Project

## Analysis Questions 
## **SQL**
**1. Retrieve the total sales for each product category**
  - The first thing i did was to create a database for this project, then load the dataset into the SQL environment
  - I decided to **SUM** the ```Sales``` as ```Total_Sales``` and group the data by the ```Product_Category```
  
     ```
     SELECT Product as Product_Category, SUM(Quantity) AS Total_Sales
     FROM LITA_Capstone_SalesData GROUP BY Product
     ```
**2. Find the number of sales transactions in each region**
  - Here, i used the ```OrderID``` to ***COUNT*** the number of transactions, and grouped by ```Region```
    ```
    SELECT Region, Count(OrderID) AS Total_Transaction
      FROM LITA_Capstone_SalesData
    GROUP BY Region
    ```

**3. Find the highest-selling product by total sales value**
  - Since we are looking for the highest, i decided to first select the **TOP 1** i then **SUM** the ```Total_Revenue```, and later **GROUP**ed by product.
  - I then arranged (**ORDER**) the results in descending order.
  - I used the ```Total_Revenue``` because the question says Value of the total sales.

    ```
    SELECT top 1 Product, SUM(Total_Revenue) AS Total_Sales
    FROM LITA_Capstone_SalesData GROUP BY Product
    ORDER BY Total_Revenue Desc
    ```
**4. Calculate total revenue per product**
  - I calculated the **SUM** of ```Total_Revenue```                                                                                                                                                                                 
    ```
    SELECT Product, SUM(Total_Revenue) AS TotalRevenue 
    FROM LITA_Capstone_SalesData GROUP BY Product
    ```
**5. Calculate monthly sales totals for the current year**
  - To solve this, i decided to filter the dataset for the current year using **GETDATE**, **GROUP** by the month.
  - Calculated the **SUM** of the ```Quantity``` for each month, and finally order the results by month.
   ``` 
    SELECT MONTH(OrderDate) AS Month, SUM(Quantity) AS Total_Sales
    FROM LITA_Capstone_SalesData WHERE YEAR(OrderDate) = YEAR(GETDATE())
    GROUP BY MONTH(OrderDate)
    ORDER BY MONTH(OrderDate)
  ```
**6. Find the top 5 customers by total purchase amount**
  - I decided to first select the **TOP 5**, so that the results given after the querry will be limited to just the top 5.
  - I then **SUM** the ```Total_Revenue```, and **GROUP BY** ```Customer_Id```.
  - I finally arranged it (**ORDER**) by the ```Total_Sales``` in descending order.
    ```
    SELECT top 5 Customer_Id, SUM(Total_Revenue) AS Total_Sales
    FROM LITA_Capstone_SalesData GROUP BY Customer_Id
    ORDER BY Total_Sales Desc
    ```
**7. Calculate the percentage of total sales contributed by each region**
  - To get the percentage, i divided the Regional total sales by the total sales for all the regions multiplied by 100
  ```
    SELECT Region, SUM(Total_Revenue) AS TotalSales,
    SUM(Total_Revenue) * 100 / SUM(SUM(Total_Revenue)) OVER ()  AS Percentage_TotalSales
    FROM LITA_Capstone_SalesData
    GROUP BY Region
   ``` 
**8. identify products with no sales in the last quarter
  - I filtered the data for the last quarter in the current date using **DATEPART** to extract the quarter and also calculated the 3 months prior to the current date, which will also represent the beginning of the last quarter as well.
  - Then **GROUP** by ```Product```
  - Identified the product with zero (0) sales using **HAVING COUNT(*) = 0**
  - No products was returned after executing the query which means that there are no product with 0 sales in the last quarter.
    ```
    SELECT Product
    FROM LITA_Capstone_SalesData
    WHERE DATEPART(QUARTER, OrderDate) = DATEPART(QUARTER, DATEADD(MONTH, -3, GETDATE())) AND YEAR(OrderDate) = YEAR(GETDATE)))
    GROUP BY Product
    HAVING COUNT(*) = 0
    ```

     
