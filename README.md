# kachajanvi-SQL_PR_1_Data_Digger

# Data Digger – MySQL Database Project

## 📌 Project Overview

**Data Digger** is a MySQL database project designed to manage customer, product, order, and order-detail information.

The database contains four main tables:

* `customers`
* `products`
* `orders`
* `orderdetails`

These tables are connected using **Primary Keys** and **Foreign Keys** to maintain relationships between customers, orders, and products.

---

## 🗄️ Database Information

**Database Name:** `data_digger`

**Database System:** MySQL

**Server Version:** MySQL 9.7.2

**Character Set:** UTF-8 (`utf8mb4`)

**Storage Engine:** InnoDB

---

## 📂 Database Structure

The database contains the following tables:

### 1. Customers Table

The `customers` table stores information about customers.

| Column     | Data Type    | Description           |
| ---------- | ------------ | --------------------- |
| CustomerID | INT          | Unique ID of customer |
| Name       | VARCHAR(50)  | Customer name         |
| Email      | VARCHAR(100) | Customer email        |
| Address    | VARCHAR(150) | Customer address      |

### Constraints

* `CustomerID` is the **Primary Key**.
* `Email` has a **UNIQUE** constraint.
* `Name` cannot be NULL.

### Sample Customers

| CustomerID | Name  | Email                                     | Address   |
| ---------: | ----- | ----------------------------------------- | --------- |
|          1 | Rahul | [rahul@gmail.com](mailto:rahul@gmail.com) | Vapi      |
|          2 | Neha  | [neha@gmail.com](mailto:neha@gmail.com)   | Ahmedabad |
|          3 | Karan | [karan@gmail.com](mailto:karan@gmail.com) | Vadodara  |
|          4 | Pooja | [pooja@gmail.com](mailto:pooja@gmail.com) | Rajkot    |

---

## 2. Products Table

The `products` table stores information about products available in the system.

| Column      | Data Type     | Description       |
| ----------- | ------------- | ----------------- |
| ProductID   | INT           | Unique product ID |
| ProductName | VARCHAR(100)  | Name of product   |
| Price       | DECIMAL(10,2) | Product price     |
| Stock       | INT           | Available stock   |

### Sample Products

| ProductID | ProductName  |   Price | Stock |
| --------: | ------------ | ------: | ----: |
|       201 | Gaming Mouse |  900.00 |    20 |
|       202 | Keyboard     | 1500.00 |    12 |
|       203 | Earphones    | 1100.00 |    25 |
|       204 | Laptop Stand | 1400.00 |     8 |

---

## 3. Orders Table

The `orders` table stores customer order information.

| Column      | Data Type     | Description                   |
| ----------- | ------------- | ----------------------------- |
| OrderID     | INT           | Unique order ID               |
| CustomerID  | INT           | Customer who placed the order |
| OrderDate   | DATE          | Date of order                 |
| TotalAmount | DECIMAL(10,2) | Total order amount            |

### Constraints

* `OrderID` is the **Primary Key**.
* `CustomerID` is a **Foreign Key** referencing `customers(CustomerID)`.

### Sample Orders

| OrderID | CustomerID | OrderDate  | TotalAmount |
| ------: | ---------: | ---------- | ----------: |
|     101 |          1 | 2026-08-02 |     2400.00 |
|     102 |          2 | 2026-08-07 |     1500.00 |
|     103 |          3 | 2026-08-12 |     3200.00 |
|     104 |          4 | 2026-08-17 |      900.00 |

---

## 4. OrderDetails Table

The `orderdetails` table stores individual products included in each order.

| Column        | Data Type     | Description            |
| ------------- | ------------- | ---------------------- |
| OrderDetailID | INT           | Unique order detail ID |
| OrderID       | INT           | Related order          |
| ProductID     | INT           | Related product        |
| Quantity      | INT           | Quantity purchased     |
| SubTotal      | DECIMAL(10,2) | Subtotal amount        |

### Constraints

* `OrderDetailID` is the **Primary Key**.
* `OrderID` is a **Foreign Key** referencing `orders(OrderID)`.
* `ProductID` is a **Foreign Key** referencing `products(ProductID)`.

### Sample Order Details

| OrderDetailID | OrderID | ProductID | Quantity | SubTotal |
| ------------: | ------: | --------: | -------: | -------: |
|           301 |     101 |       201 |        2 |  1800.00 |
|           302 |     101 |       202 |        1 |  1600.00 |
|           303 |     102 |       203 |        1 |  1100.00 |
|           304 |     103 |       204 |        2 |  2800.00 |
|           305 |     104 |       201 |        1 |   900.00 |

---

## 🔗 Table Relationships

The database uses foreign keys to connect the tables.

```text
Customers
    |
    | CustomerID
    ↓
Orders
    |
    | OrderID
    ↓
OrderDetails
    |
    | ProductID
    ↓
Products
```

### Relationship Details

**Customers → Orders**

One customer can have multiple orders.

```text
customers.CustomerID
        ↓
orders.CustomerID
```

**Orders → OrderDetails**

One order can contain multiple order-detail records.

```text
orders.OrderID
        ↓
orderdetails.OrderID
```

**Products → OrderDetails**

One product can appear in multiple order-detail records.

```text
products.ProductID
        ↓
orderdetails.ProductID
```

---

## 🔑 Keys Used

### Primary Key

Primary keys uniquely identify records.

* `customers.CustomerID`
* `products.ProductID`
* `orders.OrderID`
* `orderdetails.OrderDetailID`

### Foreign Keys

Foreign keys establish relationships between tables.

* `orders.CustomerID` → `customers.CustomerID`
* `orderdetails.OrderID` → `orders.OrderID`
* `orderdetails.ProductID` → `products.ProductID`

---

## 🛠️ Technologies Used

* **MySQL**
* **SQL**
* **InnoDB Storage Engine**
* **UTF-8 / utf8mb4 Character Set**

---

## 🚀 How to Use the Database

### Step 1: Open MySQL

Open MySQL Workbench, MySQL Command Line, or another MySQL client.

### Step 2: Create the Database

```sql
CREATE DATABASE data_digger;
```

### Step 3: Select the Database

```sql
USE data_digger;
```

### Step 4: Import the SQL File

Run the provided SQL dump file.

For MySQL Command Line:

```sql
SOURCE data_digger.sql;
```

After importing, the four tables will be created with their sample records.

---

## 🔍 Basic SQL Queries

### Display All Customers

```sql
SELECT * FROM customers;
```

### Display All Products

```sql
SELECT * FROM products;
```

### Display All Orders

```sql
SELECT * FROM orders;
```

### Display Order Details

```sql
SELECT * FROM orderdetails;
```

---

## 🔗 Join Customers and Orders

To display customer names with their orders:

```sql
SELECT
    c.Name,
    o.OrderID,
    o.OrderDate,
    o.TotalAmount
FROM customers c
JOIN orders o
ON c.CustomerID = o.CustomerID;
```

---

## 🛒 Display Product Details in Orders

```sql
SELECT
    o.OrderID,
    p.ProductName,
    od.Quantity,
    od.SubTotal
FROM orderdetails od
JOIN orders o
ON od.OrderID = o.OrderID
JOIN products p
ON od.ProductID = p.ProductID;
```

---

## 💰 Calculate Total Sales

```sql
SELECT SUM(TotalAmount) AS TotalSales
FROM orders;
```

---

## 📦 Check Product Stock

```sql
SELECT
    ProductName,
    Stock
FROM products;
```

---

## 📊 Find the Most Expensive Product

```sql
SELECT *
FROM products
ORDER BY Price DESC
LIMIT 1;
```

---

## 👤 Find Customer Orders

```sql
SELECT
    c.Name,
    COUNT(o.OrderID) AS TotalOrders
FROM customers c
LEFT JOIN orders o
ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.Name;
```

---

## 🎯 Project Objectives

The main objectives of the Data Digger project are:

1. To store customer information.
2. To maintain product information.
3. To record customer orders.
4. To maintain individual order details.
5. To establish relationships between different tables.
6. To practice Primary Keys and Foreign Keys.
7. To perform SQL queries using multiple tables.
8. To retrieve useful information using JOIN operations.
9. To calculate sales and order-related information.
10. To understand relational database management using MySQL.

---

## ✅ Database Features

* Customer management
* Product management
* Order management
* Order detail management
* Primary key constraints
* Foreign key constraints
* Unique email validation
* Decimal values for prices and totals
* Relational table structure
* SQL JOIN operations
* Sales calculations
* Product stock tracking

---

## 📁 Project File Structure

A simple project structure can be:

```text
Data-Digger/
│
├── data_digger.sql
├── README.md
└── screenshots/
    ├── customers.png
    ├── products.png
    ├── orders.png
    └── orderdetails.png
```

---

## 📝 Conclusion

The **Data Digger** project demonstrates how a relational database can be designed and managed using MySQL. It uses four related tables to store customers, products, orders, and order details.

Primary keys provide unique identification for records, while foreign keys maintain relationships between the tables. The database can also be used to practice SQL operations such as `SELECT`, `JOIN`, `SUM`, `COUNT`, `GROUP BY`, and `ORDER BY`.

This project provides a practical example of database design and SQL query implementation for an order-management system.
