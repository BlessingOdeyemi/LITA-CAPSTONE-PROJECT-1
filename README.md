# LITA-CAPSTONE-PROJECT-1
This is where i document the process of answering the LITA Capstone Project

### Sales Performance Analysis for a Retail Store

## Analysis Questions 
## **SQL**
**1. Retrieve the total sales for each product category**
  - The first thing i did was to create a database for this project, then load the dataset into the SQL environment
  - I decided to **SUM** the ```Sales``` as ```Total_Sales``` and group the data by the ```Product_Category```
  
     ```
     SELECT Product as Product_Category, SUM(Quantity) AS Total_Sales
     FROM LITA_Capstone_SalesData GROUP BY Product
     ```
     ![SQL_Sales1 right](https://github.com/user-attachments/assets/2a1423c3-59a0-4285-bae6-b4d957451169)

**2. Find the number of sales transactions in each region**
  - Here, i used the ```OrderID``` to ***COUNT*** the number of transactions, and grouped by ```Region```
    ```
    SELECT Region, Count(OrderID) AS Total_Transaction
      FROM LITA_Capstone_SalesData
    GROUP BY Region
    ```
![SQL_Sales 2](https://github.com/user-attachments/assets/389f352a-3739-4301-b33b-376726d96201)

**3. Find the highest-selling product by total sales value**
  - Since we are looking for the highest, i decided to first select the **TOP 1** i then **SUM** the ```Total_Revenue```, and later **GROUP**ed by product.
  - I then arranged (**ORDER**) the results in descending order.
  - I used the ```Total_Revenue``` because the question says Value of the total sales.

    ```
    SELECT top 1 Product, SUM(Total_Revenue) AS Total_Sales
    FROM LITA_Capstone_SalesData GROUP BY Product
    ORDER BY Total_Revenue Desc
    ```
![SQL_Sales 3](https://github.com/user-attachments/assets/b18e449b-ddb8-49c1-9f00-1bb7332566a6)

    
**4. Calculate total revenue per product**
  - I calculated the **SUM** of ```Total_Revenue```                                                                                                                                                                                 
    ```
    SELECT Product, SUM(Total_Revenue) AS TotalRevenue 
    FROM LITA_Capstone_SalesData GROUP BY Product
    ```
![SQL_Sales 4](https://github.com/user-attachments/assets/212c1d10-eb9f-4f13-8ffb-cde792c3ea23)

Shoes has brought in the highst revenue (613,380) so far, concentration should be placed on Socks to help push sales

**5. Calculate monthly sales totals for the current year**
  - To solve this, i decided to filter the dataset for the current year using **GETDATE**, **GROUP** by the month.
  - Calculated the **SUM** of the ```Quantity``` for each month, and finally order the results by month.
   ``` 
    SELECT MONTH(OrderDate) AS Month, SUM(Quantity) AS Total_Sales
    FROM LITA_Capstone_SalesData WHERE YEAR(OrderDate) = YEAR(GETDATE())
    GROUP BY MONTH(OrderDate)
    ORDER BY MONTH(OrderDate)
  ```
![SQL_Sales 5](https://github.com/user-attachments/assets/9b698a98-6709-40d9-8b78-c5a49d37a73c)

June has records the highest sales in 2024 so far

**6. Find the top 5 customers by total purchase amount**
  - I decided to first select the **TOP 5**, so that the results given after the querry will be limited to just the top 5.
  - I then **SUM** the ```Total_Revenue```, and **GROUP BY** ```Customer_Id```.
  - I finally arranged it (**ORDER**) by the ```Total_Sales``` in descending order.
    ```
    SELECT top 5 Customer_Id, SUM(Total_Revenue) AS Total_Sales
    FROM LITA_Capstone_SalesData GROUP BY Customer_Id
    ORDER BY Total_Sales Desc
    ```
![SQL_Sales 6](https://github.com/user-attachments/assets/22230ab0-7bc0-4858-99af-ad66113e72ba)

These 5 customers have the top purchasing amount, which conincidentaly is the same amount
    
**7. Calculate the percentage of total sales contributed by each region**
  - To get the percentage, i divided the Regional total sales by the total sales for all the regions multiplied by 100
  ```
    SELECT Region, SUM(Total_Revenue) AS TotalSales,
    SUM(Total_Revenue) * 100 / SUM(SUM(Total_Revenue)) OVER ()  AS Percentage_TotalSales
    FROM LITA_Capstone_SalesData
    GROUP BY Region
   ```
![SQL_Sales 7](https://github.com/user-attachments/assets/fc0de954-e25e-462b-95ca-6e8b997a717e)

This indicates that the South Region recorded the highest sales

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
     ![SQL_Sales 8](https://github.com/user-attachments/assets/1e6e135b-906e-470f-ab28-06fe588ea1c6)

    There are no product with zero sales

## **EXCEL**
![Piv_1](https://github.com/user-attachments/assets/4bfb8762-fe2d-4f6b-9dfe-4fd714c32c5e)

![Piv 2](https://github.com/user-attachments/assets/420cade9-9651-41fe-b6f8-142617b3d5a3)

![Piv_3](https://github.com/user-attachments/assets/7d950316-76bc-460d-baa7-05f6c87a07c5)



![Exc_Avg](https://github.com/user-attachments/assets/bf86234e-dc34-4198-a6fb-f636a50da822)

![Exc_Total Rev](https://github.com/user-attachments/assets/7b1ab6df-e0bb-4dc9-b451-c6d0027899b2)


![Chart 1](https://github.com/user-attachments/assets/aa1f260b-e5cb-4642-8bb1-0e53e37cb20f)


