E-Commerce Database Management System

📌 Project Overview

This project is a relational E-Commerce Database Management System developed using SQL.
The database is designed to manage essential e-commerce information including users, products, orders, order items, payments, and product reviews.
The project demonstrates the use of database creation, table design, primary keys, foreign keys, data insertion, filtering, aggregation, and SQL JOIN operations.

🎯 Objective

The main objectives of this project are:
Design a relational database for an e-commerce application.
Store and manage customer information.
Maintain product and inventory information.
Manage customer orders and order items.
Track payment information.
Store product reviews and ratings.
Retrieve meaningful information using SQL queries.
Understand relationships between multiple database tables.

🛠️ Technologies Used

SQL
Relational Database
Primary Keys
Foreign Keys
INNER JOIN
LEFT JOIN
WHERE
GROUP BY
COUNT()
SUM()

🗄️ Database Structure

The database is named:
ecommerce
The project contains six main tables:
Table	Purpose
userr	Stores customer information
prodts	Stores product details and stock
ordered	Stores customer order information
itemss	Stores products associated with orders
pay	Stores payment details
revives	Stores customer product reviews
The tables are connected using primary and foreign key relationships.

🔗 Database Relationships
               
                USER
                 |
                 | user_id
                 |
                 v
               ORDER
              /     \
             /       \
            v         v
      ORDER ITEMS   PAYMENT
          |
          | product_id
          v
       PRODUCT
          ^
          |
       REVIEW
          |
       user_id
Relationships
One user can have multiple orders.
An order can contain multiple order items.
Each order item is associated with a product.
An order can have payment information.
Users can submit reviews for products.

📋 Table Details

1. Users
The userr table stores customer information such as:
User ID
Name
Email
Phone
Address
Date of joining

CREATE TABLE userr (
    user_id INT PRIMARY KEY,
    name VARCHAR(20),
    email VARCHAR(30),
    phone VARCHAR(15),
    address TEXT,
    doj DATE
);

2. Products
The prodts table stores product information including:
Product ID
Product name
Category
Price
Stock
Description
Added date

CREATE TABLE prodts (
    product_id INT PRIMARY KEY,
    name VARCHAR(20),
    category VARCHAR(30),
    price FLOAT,
    stock INT,
    desrc TEXT,
    added_date DATE
);

3. Orders
The ordered table stores customer order information.

CREATE TABLE ordered (
    order_id INT PRIMARY KEY,
    user_id INT,
    order_date DATE,
    total_amount FLOAT,
    statue VARCHAR(10),
    FOREIGN KEY (user_id) REFERENCES userr(user_id)
);

4. Order Items
The itemss table connects orders with products and stores the quantity and price.

CREATE TABLE itemss (
    item_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    price FLOAT,
    FOREIGN KEY (order_id) REFERENCES ordered(order_id),
    FOREIGN KEY (product_id) REFERENCES prodts(product_id)
);

5. Payments
The pay table stores payment information such as payment type, status, and date.

CREATE TABLE pay (
    payment_id INT PRIMARY KEY,
    order_id INT,
    payment_type VARCHAR(10),
    statue VARCHAR(7),
    payment_date DATE,
    FOREIGN KEY (order_id) REFERENCES ordered(order_id)
);

6. Reviews
The revives table stores customer reviews and ratings for products.

CREATE TABLE revives (
    review_id INT PRIMARY KEY,
    user_id INT,
    product_id INT,
    rating INT,
    comt TEXT,
    review_date DATE,
    FOREIGN KEY (user_id) REFERENCES userr(user_id),
    FOREIGN KEY (product_id) REFERENCES prodts(product_id)
);

The project includes sample data for users, products, orders, payments, and reviews.

🔍 SQL Queries Implemented

Filtering Data
Retrieve users who joined after a specific date:

SELECT *
FROM userr
WHERE doj > '2024-07-01';

Retrieve orders belonging to a specific user:

SELECT *
FROM ordered
WHERE user_id = 3;

Retrieve products based on stock:

SELECT *
FROM prodts
WHERE stock < 1000;

📊 Aggregate Queries
Calculate the total value of order items:

SELECT SUM(price * quantity)
FROM itemss;

Count users:

SELECT COUNT(user_id)
FROM userr
GROUP BY user_id;

The project also includes queries for filtering reviews by rating and retrieving payment information.

🔗 JOIN Operations

INNER JOIN
The project uses an INNER JOIN to retrieve users together with their corresponding orders.

SELECT u.user_id,
       u.name,
       o.order_id,
       o.order_date,
       o.total_amount
FROM userr u
INNER JOIN ordered o
ON u.user_id = o.user_id;
This allows customer information and order information to be retrieved together.

LEFT JOIN
A LEFT JOIN is used to retrieve all users, including users who may not have a matching order.

SELECT u.user_id,
       u.name,
       o.order_id,
       o.total_amount
FROM userr u
LEFT JOIN ordered o
ON u.user_id = o.user_id;
The project also uses a LEFT JOIN to identify products that do not appear in the order items table.

✨ Key Features

Relational database design
Customer management
Product management
Order management
Order-item relationships
Payment tracking
Product reviews and ratings
Primary and foreign key constraints
Data filtering
Aggregate functions
INNER JOIN queries
LEFT JOIN queries

📚 Key Learnings

Through this project, I gained practical experience in:

Creating and managing relational databases
Designing tables and relationships
Using primary and foreign keys
Inserting and retrieving data
Writing SQL filtering queries
Using aggregate functions
Working with INNER JOIN and LEFT JOIN
Understanding relationships between multiple tables
Retrieving useful information from structured data

📁 Project Structure

ecommerce-database/
│
├── ecommerce.sql
└── README.md

The ecommerce.sql file contains the database creation, table definitions, sample data, and SQL queries used in the project.

🚀 Future Improvements

Add stored procedures
Add database views
Add triggers for inventory management
Add more advanced analytical queries
Create a frontend application connected to the database
Add an API layer for accessing the database
Implement authentication and authorization

📌 Project Status

Completed

This project demonstrates the design and querying of a relational e-commerce database using SQL.
