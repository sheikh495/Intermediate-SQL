# Customer Orders Database Project

This project demonstrates how to create and manipulate an SQLite database using Python in Google Colab. It includes the creation of database tables, data insertion, and performing various SQL queries on a simulated customer orders database.

## Project Overview

The project is divided into two main parts:
1. **Creating the Database Tables and Inserting Data**
2. **Writing SQL Queries to Manipulate and Analyze Data**

### 1. Creating the Database Tables and Inserting Data

In this section, two tables are created:

- **Customers Table**: Contains customer information such as CustomerID, CustomerName, and Country.
- **Orders Table**: Contains order information, including OrderID, CustomerID (as a foreign key), OrderDate, and TotalAmount.

After creating the tables, data for several customers and their respective orders are inserted into the database.

### 2. Writing SQL Queries

The second part of the project involves writing various SQL queries to explore and manipulate the data in the tables. Below are the problem statements and detailed solutions:

#### Problem 1: Customer Orders with Conditional Logic

**Task**: Write a query that returns the `CustomerName`, `Country`, `TotalAmount`, and a new column named `OrderCategory`. Use a `CASE` statement to categorize orders:
- "High" if `TotalAmount` > 150
- "Medium" if `TotalAmount` between 100 and 150
- "Low" if `TotalAmount` < 100

**Solution**:
```sql
SELECT
  c.CustomerName,
  c.Country,
  o.TotalAmount,
  CASE
    WHEN o.TotalAmount > 150 THEN 'High'
    WHEN o.TotalAmount BETWEEN 100 AND 150 THEN 'Medium'
    ELSE 'Low'
  END AS OrderCategory
FROM
  Customers c
JOIN
  Orders o
ON
  c.CustomerID = o.CustomerID;
```
This query categorizes each order based on the `TotalAmount` column.

#### Problem 2: Grouping and Aggregation by Country

**Task**: Return each `Country` and the total number of orders placed by customers in that country, but only include countries that have placed more than one order.

**Solution**:
```sql
SELECT
  c.Country,
  COUNT(o.OrderID) AS TotalOrders
FROM
  Customers c
JOIN
  Orders o
ON
  c.CustomerID = o.CustomerID
GROUP BY
  c.Country
HAVING
  COUNT(o.OrderID) > 1;
```
This query counts the number of orders placed in each country and filters out countries with only one order using the `HAVING` clause.

#### Problem 3: Combining Tables with Joins

**Task**: Return the `CustomerName`, `OrderID`, and `TotalAmount` for all customers, including those who haven’t placed an order. Use a `LEFT JOIN` to ensure all customers are listed.

**Solution**:
```sql
SELECT
  c.CustomerName,
  o.OrderID,
  o.TotalAmount
FROM
  Customers c
LEFT JOIN
  Orders o
ON
  c.CustomerID = o.CustomerID;
```
This query uses a `LEFT JOIN` to return all customers, showing `NULL` for `OrderID` and `TotalAmount` where no orders have been placed.

#### Problem 4: Subqueries

**Task**: Write a query that returns the `CustomerName` and `TotalAmount` for customers whose total order amount exceeds the average order amount across all customers. Use a subquery to calculate the average.

**Solution**:
```sql
SELECT
  c.CustomerName,
  o.TotalAmount
FROM
  Customers c
JOIN
  Orders o
ON
  c.CustomerID = o.CustomerID
WHERE
  o.TotalAmount > (SELECT AVG(TotalAmount) FROM Orders);
```
This query filters customers whose `TotalAmount` exceeds the average of all order totals, using a subquery in the `WHERE` clause.

#### Problem 5: Using a CTE for Average Order Amount

**Task**: Write a query using a CTE (Common Table Expression) that calculates the average order amount per country and then selects the customers who have an order amount above their country’s average.

**Solution**:
```sql
WITH CountryAvg AS (
  SELECT
    c.Country,
    AVG(o.TotalAmount) AS AvgAmount
  FROM
    Customers c
  JOIN
    Orders o
  ON
    c.CustomerID = o.CustomerID
  GROUP BY
    c.Country
)
SELECT
  c.CustomerName,
  o.TotalAmount,
  ca.AvgAmount
FROM
  Customers c
JOIN
  Orders o
ON
  c.CustomerID = o.CustomerID
JOIN
  CountryAvg ca
ON
  c.Country = ca.Country
WHERE
  o.TotalAmount > ca.AvgAmount;
```
This query uses a `WITH` clause to define a CTE called `CountryAvg` that calculates the average order amount for each country. The main query then joins the result of the CTE with the orders table to find customers whose order totals exceed their country's average.

### Requirements

To run this project in Google Colab, you don't need any external dependencies beyond Python, SQLite, and the `tabulate` library for better display of results in a table format. Here's how you can get started:

1. **Google Colab**  
   Open the project in Google Colab. All the code can be run directly in Colab, which supports SQLite by default.

2. **Python Libraries**  
   You may need to install the `tabulate` library for better formatting of output:
   ```python
   !pip install tabulate
   ```

### Running the Project

To run the project, follow these steps:

1. Clone or download the `.ipynb` notebook file.
2. Open the notebook in Google Colab.
3. Run each code cell sequentially:
   - The first few cells will create the database tables and insert data.
   - The remaining cells will perform the SQL queries and display the results.

### Folder Structure

```
customer-orders-database/
│
├── README.md          # Project overview and instructions
├── customer_orders.ipynb # Python notebook with the SQLite database code
```

### Example Output

After running the queries, you'll see outputs in tabular format displaying customer names, countries, order totals, and various other requested data.

### Notes

- The database created is stored in-memory, which means it won't persist after the notebook runtime ends.
- You can modify the queries or add more customers and orders to explore the data further.

### License

This project is open-source and available under the [MIT License](https://opensource.org/licenses/MIT).

---


