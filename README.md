# projectDB
Coursera database course project

Writing Basic SQL Queries with Microsoft Copilot:
A database to store and retrieve inventory data efficiently.
Initial STEPS:
To create a database for a store inventory system using MySQL CLI in Visual Studio, follow these steps:

### 1. Install MySQL and Set Up Visual Studio
- Download and install MySQL Server and MySQL Workbench from [MySQL's official site](https://dev.mysql.com/downloads/).
- Install MySQL Connector for .NET to allow Visual Studio to interact with MySQL.
- Ensure Visual Studio is installed with the necessary database management extensions.

### 2. Open MySQL CLI and Create the Database
1. Open the MySQL Command Line Client or use a terminal with MySQL installed.
2. Log in to MySQL:
   ```sh
   mysql -u root -p
   ```
3. Create a new database:
   ```sql
   CREATE DATABASE store_inventory;
   ```
4. Select the database:
   ```sql
   USE store_inventory;
   ```

### 3. Create Tables for Inventory Management
Define tables for products, stock, and transactions:
```sql
CREATE TABLE products (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    stock_quantity INT NOT NULL
);

CREATE TABLE transactions (
    transaction_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT,
    quantity INT NOT NULL,
    transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

### 4. Connect MySQL to Visual Studio
- Open Visual Studio and create a new project (C# or VB.NET).
- Install MySQL.Data package via NuGet:
  ```sh
  Install-Package MySql.Data
  ```
- Establish a connection in your application:
  ```csharp
  using MySql.Data.MySqlClient;

  string connectionString = "server=localhost;user=root;password=yourpassword;database=store_inventory;";
  MySqlConnection conn = new MySqlConnection(connectionString);
  conn.Open();
  Console.WriteLine("Connected to MySQL database!");
  ```

### 5. Implement CRUD Operations
- Write functions to add, update, delete, and retrieve inventory data.
- Use SQL queries within your application to interact with the database.

For a complete inventory system with a user interface, you can check out this [Inventory Management System](https://www.sourcecodester.com/visual-basic-net/12898/inventory-management-system-using-visual-basic-2015-and-mysql-database.html) built with VB.NET and MySQL.

Adding a Category Column

Great! To add a **product categories** table and link it to the **products** table, follow these steps:
### 1. Create the `categories` Table
Run the following SQL command in MySQL CLI:
```sql
CREATE TABLE categories (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(255) NOT NULL
);
```

### 2. Modify the `products` Table to Include a Category Reference
Add a foreign key to link products to categories:
```sql
ALTER TABLE products ADD COLUMN category_id INT;
ALTER TABLE products ADD CONSTRAINT fk_category FOREIGN KEY (category_id) REFERENCES categories(category_id);
```

### 3. Insert Sample Categories
Add some initial categories:
```sql
INSERT INTO categories (category_name) VALUES ('Electronics'), ('Clothing'), ('Groceries');
```

### 4. Insert Products with Categories
Include `category_id` when adding products:
```sql
INSERT INTO products (name, description, price, stock_quantity, category_id) 
VALUES ('Laptop', '15-inch screen laptop', 999.99, 10, 1);
```

### 5. Retrieve Products with Category Information
Join the tables to fetch products with their category names:
```sql
SELECT p.product_id, p.name, p.description, p.price, p.stock_quantity, c.category_name
FROM products p
JOIN categories c ON p.category_id = c.category_id;
```
ADDING MORE PRODUCTS
initial request:
INSERT INTO products (name, description, price, stock_quantity, category_id) VALUES ('Laptop - 18', '18-inch screen laptop', 1999.99, 10, 1), ('Television' – Plasma’, 'Plasma 85-inch screen television', 2999.99, 10, 1) , ('Shirt Sleeve Shirt – M’, 'Shirt Sleeve Shirt – M’, 19.99, 10, 2) , ('Bermuda Shorts - M', ' Bermuda Shorts - M ', 59.99, 15, 2) , ('Television - LED', 'LED 85-inch screen television', 1999.99, 10, 1) , ('Laptop', '15-inch screen laptop', 999.99, 10, 1) , ('Peanut Butter', '18-ounce jar of peanut butter', 9.99, 10, 3) , ('Eggs – 1 dozen', '1 carton of a dozen eggs', 19.99, 10, 3) , ('Necktie - Red', 'Red Necktie’, 999.99, 10, 2); is the code above the correct way to add multiple items to the products table
Co-pilot response:
There are a few syntax errors in your SQL query that need correction:

### Issues:
1. Incorrect usage of **special characters (`–`, `’`)**:
   - Replace **en dashes (–)** and **smart quotes (`’`)** with standard hyphens (`-`) and regular single quotes (`'`).
2. Incorrect **quote placement** in `'Television' – Plasma’` and `'Necktie - Red', 'Red Necktie’'`.
3. Extra spaces in `' Bermuda Shorts - M '`.

### Corrected SQL Code:
```sql
INSERT INTO products (name, description, price, stock_quantity, category_id) 
VALUES 
('Laptop - 18', '18-inch screen laptop', 1999.99, 10, 1), 
('Television - Plasma', 'Plasma 85-inch screen television', 2999.99, 10, 1), 
('Short Sleeve Shirt - M', 'Short Sleeve Shirt - M', 19.99, 10, 2), 
('Bermuda Shorts - M', 'Bermuda Shorts - M', 59.99, 15, 2), 
('Television - LED', 'LED 85-inch screen television', 1999.99, 10, 1), 
('Laptop', '15-inch screen laptop', 999.99, 10, 1), 
('Peanut Butter', '18-ounce jar of peanut butter', 9.99, 10, 3), 
('Eggs - 1 dozen', '1 carton of a dozen eggs', 19.99, 10, 3), 
('Necktie - Red', 'Red Necktie', 999.99, 10, 2);
```
### Summary of Fixes:
✔ Used **correct single quotes `'`** instead of `’`  
✔ Replaced **en dashes `–`** with standard hyphens `-`  
✔ Fixed **misplaced quotes**  
✔ Removed **unnecessary spaces**  

This corrected query should now properly insert multiple items into the `products` table without syntax errors.

PRODUCT QUERY:
Question for co-pilor:
yes, how would query be written, when i need to list out all product with a price under 50.

RESPONSE:
You can use the `SELECT` statement with a `WHERE` clause to filter products by price:

```sql
SELECT product_id, name, description, price, stock_quantity, category_id
FROM products
WHERE price < 50;
```

### Explanation:
- `SELECT`: Retrieves data from the `products` table.
- `WHERE price < 50`: Filters the results to only include products priced below **$50**.
