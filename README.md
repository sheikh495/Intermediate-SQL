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

The second part of the project involves writing various SQL queries to explore and manipulate the data in the tables:

- **Problem 1: Customer Orders with Conditional Logic**  
  Categorizes each order into "High", "Medium", or "Low" based on the total amount of the order.

- **Problem 2: Grouping and Aggregation by Country**  
  Groups orders by country and returns the total number of orders per country where the total number of orders is greater than one.

- **Problem 3: Combining Tables with Joins**  
  Uses a `LEFT JOIN` to combine the Customers and Orders tables, ensuring all customers are listed even if they haven't placed any orders.

- **Problem 4: Subqueries**  
  Finds customers whose total order amount exceeds the average order amount across all customers using a subquery.

- **Problem 5: Using a CTE (Common Table Expression)**  
  Calculates the average order amount per country using a CTE and returns customers with an order amount above their country’s average.

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
