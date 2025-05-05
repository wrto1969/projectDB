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
### i would like to create a table for product categories and include it in the products table what are the next steps i should do
1. Create the categories Table
Run the following SQL command in MySQL CLI:

CREATE TABLE categories (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(255) NOT NULL
);
2. Modify the products Table to Include a Category Reference
Add a foreign key to link products to categories:

ALTER TABLE products ADD COLUMN category_id INT;
ALTER TABLE products ADD CONSTRAINT fk_category FOREIGN KEY (category_id) REFERENCES categories(category_id);

3. Insert Sample Categories
Add some initial categories:
INSERT INTO categories (category_name) VALUES ('Electronics'), ('Clothing'), ('Groceries');

4. Insert Products with Categories
Include category_id when adding products:
INSERT INTO products (name, description, price, stock_quantity, category_id) 
VALUES ('Laptop', '15-inch screen laptop', 999.99, 10, 1);

5. Retrieve Products with Category Information
Join the tables to fetch products with their category names:
SELECT p.product_id, p.name, p.description, p.price, p.stock_quantity, c.category_name
FROM products p
JOIN categories c ON p.category_id = c.category_id;

### INSERT INTO products (name, description, price, stock_quantity, category_id) VALUES ('Laptop - 18', '18-inch screen laptop', 1999.99, 10, 1), ('Television' – Plasma’, 'Plasma 85-inch screen television', 2999.99, 10, 1) , ('Shirt Sleeve Shirt – M’, 'Shirt Sleeve Shirt – M’, 19.99, 10, 2) , ('Bermuda Shorts - M', ' Bermuda Shorts - M ', 59.99, 15, 2) , ('Television - LED', 'LED 85-inch screen television', 1999.99, 10, 1) , ('Laptop', '15-inch screen laptop', 999.99, 10, 1) , ('Peanut Butter', '18-ounce jar of peanut butter', 9.99, 10, 3) , ('Eggs – 1 dozen', '1 carton of a dozen eggs', 19.99, 10, 3) , ('Necktie - Red', 'Red Necktie’, 999.99, 10, 2); is the code above the correct way to add multiple items to the products table
There are a few syntax errors in your SQL query that need correction:
Issues:
- Incorrect usage of special characters (–, ’):
- Replace en dashes (–) and smart quotes (’) with standard hyphens (-) and regular single quotes (').
- Incorrect quote placement in 'Television' – Plasma’ and 'Necktie - Red', 'Red Necktie’'.
- Extra spaces in ' Bermuda Shorts - M '.
Corrected SQL Code:
INSERT INTO products (name, description, price, stock_quantity, category_id) 
VALUES 
('Laptop - 18', '18-inch screen laptop', 1999.99, 10, 1), 
('Television - Plasma', 'Plasma 85-inch screen television', 2999.99, 10, 1), 
('Short Sleeve Shirt - M'
Corrected SQL Code:
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
Summary of Fixes:
✔ Used correct single quotes ' instead of ’
✔ Replaced en dashes – with standard hyphens -
✔ Fixed misplaced quotes
✔ Removed unnecessary spaces
This corrected query should now properly insert multiple items into the products table without syntax errors.

### how would query be written, when i need to list out all product with a price under 50.
SELECT product_id, name, description, price, stock_quantity, category_id
FROM products
WHERE price < 50;

SELECT product_id, name, description, price, stock_quantity, category_id
FROM products
WHERE category_id = 2;

Adding More Categories
INSERT INTO categories (category_name) VALUES 
('Electronics'), 
('Clothing'), 
('Groceries'), 
('Furniture'), 
('Sports Equipment'), 
('Books'), 
('Toys'), 
('Home Appliances'), 
('Automotive'), 
('Beauty & Personal Care');

Adding More Products
INSERT INTO products (name, description, price, stock_quantity, category_id) VALUES 
-- Electronics (Category 1)
('Smartphone', 'Latest model with 128GB storage', 799.99, 50, 1),
('Laptop', '15-inch screen laptop', 999.99, 30, 1),
('Smartwatch', 'Water-resistant smartwatch', 249.99, 40, 1),
('Wireless Earbuds', 'Noise-cancelling earbuds', 149.99, 50, 1),

-- Clothing (Category 2)
('Jeans - L', 'Slim fit jeans', 59.99, 100, 2),
('T-shirt - XL', 'Cotton t-shirt', 19.99, 150, 2),
('Winter Jacket', 'Insulated jacket', 129.99, 20, 2),
('Running Shoes', 'Lightweight running shoes', 89.99, 75, 2),

-- Groceries (Category 3)
('Peanut Butter', '18-ounce jar', 5.99, 200, 3),
('Milk - 1 Gallon', 'Whole milk', 3.49, 100, 3),
('Brown Bread', 'Whole grain bread', 2.99, 100, 3),
('Coffee Beans', 'Medium roast coffee beans', 14.99, 50, 3),

-- Furniture (Category 4)
('Office Desk', 'Wooden desk with drawers', 199.99, 25, 4),
('Recliner Chair', 'Leather reclining chair', 299.99, 15, 4),
('Dining Table Set', '6-seat dining table', 499.99, 10, 4),
('Bookshelf', '5-tier wooden bookshelf', 129.99, 20, 4),

-- Sports Equipment (Category 5)
('Basketball', 'Official size basketball', 29.99, 75, 5),
('Tennis Racket', 'Graphite tennis racket', 99.99, 30, 5),
('Yoga Mat', 'Non-slip yoga mat', 25.99, 50, 5),
('Dumbbells - 20lbs', 'Pair of adjustable dumbbells', 59.99, 40, 5),

-- Books (Category 6)
('Programming Book', 'Advanced C# programming book', 39.99, 20, 6),
('History Book', 'World history encyclopedia', 49.99, 15, 6),
('Fantasy Novel', 'Bestselling fantasy novel', 19.99, 30, 6),
('Science Textbook', 'Physics principles textbook', 79.99, 10, 6),

-- Toys (Category 7)
('Lego Set', '1000-piece building set', 89.99, 40, 7),
('RC Car', 'Rechargeable remote-controlled car', 49.99, 35, 7),
('Dollhouse', 'Wooden dollhouse', 79.99, 20, 7),
('Puzzle Set', '3D puzzle set', 29.99, 50, 7),

-- Home Appliances (Category 8)
('Microwave Oven', '700W digital microwave', 129.99, 15, 8),
('Vacuum Cleaner', 'Cordless vacuum cleaner', 249.99, 20, 8),
('Blender', 'Multi-speed kitchen blender', 79.99, 30, 8),
('Air Purifier', 'HEPA filter air purifier', 199.99, 25, 8),

-- Automotive (Category 9)
('Car Battery', '12V high-performance battery', 159.99, 10, 9),
('Motor Oil - 5L', 'Synthetic motor oil', 39.99, 50, 9),
('GPS Navigator', 'Touchscreen GPS with maps', 199.99, 15, 9),
('Jump Starter Kit', 'Portable car battery starter', 89.99, 20, 9),

-- Beauty & Personal Care (Category 10)
('Face Wash', 'Gentle foaming cleanser', 14.99, 50, 10),
('Shampoo - 500ml', 'Moisturizing shampoo', 9.99, 75, 10),
('Electric Hair Trimmer', 'Rechargeable trimmer', 29.99, 40, 10),
('Perfume - 100ml', 'Luxury fragrance perfume', 59.99, 30, 10);

### create a table that will be for store location one location for electronic, one location for groceries, one location  for furniture, and the last one for all categories combines. the products table is shared by the four stores like a warehouse facility.

1. Create the store_locations Table
CREATE TABLE store_locations (
    store_id INT AUTO_INCREMENT PRIMARY KEY,
    store_name VARCHAR(255) NOT NULL,
    store_address VARCHAR(255),
    category_id INT NULL, -- NULL for the store that carries all categories
    FOREIGN KEY (category_id) REFERENCES categories(category_id)
);

2. Insert Store Locations
INSERT INTO store_locations (store_name, store_address, category_id) VALUES 
('Electronics Store', '123 Tech Ave, City, State', 1), -- Electronics only
('Grocery Store', '456 Market St, City, State', 3), -- Groceries only
('Furniture Store', '789 Home Ln, City, State', 4), -- Furniture only
('Warehouse Store', '999 Central Blvd, City, State', NULL); -- Carries all categories

3. Linking Products to Store Locations
CREATE TABLE store_inventory (
    store_id INT,
    product_id INT,
    stock_quantity INT NOT NULL,
    PRIMARY KEY (store_id, product_id),
    FOREIGN KEY (store_id) REFERENCES store_locations(store_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);

4. Insert Product Stock for Each Store
INSERT INTO store_inventory (store_id, product_id, stock_quantity) VALUES 
-- Electronics Store (Store ID 1)
(1, 1, 20), (1, 2, 15), (1, 3, 30),

-- Grocery Store (Store ID 2)
(2, 9, 100), (2, 10, 50), (2, 11, 70),

-- Furniture Store (Store ID 3)
(3, 13, 10), (3, 14, 5), (3, 15, 8),

-- Warehouse Store (Store ID 4 - all products)
(4, 1, 50), (4, 9, 200), (4, 13, 25), (4, 20, 30);

Retrieving Stock Per Store
To check what products are available at a given store:
SELECT s.store_name, p.name, i.stock_quantity
FROM store_inventory i
JOIN store_locations s ON i.store_id = s.store_id
JOIN products p ON i.product_id = p.product_id
WHERE s.store_name = 'Electronics Store';

### restocking system and automatic stock adjustment
1. Create a Restocking Table
This table will track restock requests and completion status.
CREATE TABLE restock_requests (
    request_id INT AUTO_INCREMENT PRIMARY KEY,
    store_id INT,
    product_id INT,
    requested_quantity INT NOT NULL,
    status ENUM('Pending', 'Completed') DEFAULT 'Pending',
    request_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (store_id) REFERENCES store_locations(store_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);

2. Define a Minimum Stock Level Per Store
Each store can have a predefined minimum quantity per product
ALTER TABLE store_inventory ADD COLUMN min_stock_level INT DEFAULT 5;

3. Create a Trigger for Automatic Restocking
Whenever a store’s stock drops below the minimum threshold, a restock request is generated.
CREATE TRIGGER auto_restock_trigger
AFTER UPDATE ON store_inventory
FOR EACH ROW
BEGIN
    IF NEW.stock_quantity < NEW.min_stock_level THEN
        INSERT INTO restock_requests (store_id, product_id, requested_quantity)
        VALUES (NEW.store_id, NEW.product_id, (NEW.min_stock_level - NEW.stock_quantity));
    END IF;
END;

4. Handling Restock Requests
When a request is fulfilled (stock is updated), mark it as completed
UPDATE restock_requests 
SET status = 'Completed' 
WHERE request_id = 1;

5. Automatically Adjust Stock Upon Restocking
When a request is completed, update store_inventory:
UPDATE store_inventory 
SET stock_quantity = stock_quantity + 10
WHERE store_id = 1 AND product_id = 2;

### create a sales table with at 30 customers pasts order going back 3 months.
1. Create the sales Table
CREATE TABLE sales (
    sale_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(255) NOT NULL,
    product_id INT NOT NULL,
    store_id INT NOT NULL,
    quantity INT NOT NULL,
    total_price DECIMAL(10,2) NOT NULL,
    sale_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES products(product_id),
    FOREIGN KEY (store_id) REFERENCES store_locations(store_id)
);

2. Insert Sample Sales Data (Going Back 3 Months)
Each sale entry records: ✅ Customer Name
✅ Product Purchased
✅ Store Location
✅ Quantity & Total Price
✅ Sale Date (past 3 months)
INSERT INTO sales (customer_name, product_id, store_id, quantity, total_price, sale_date) VALUES 
-- Sales from January
('Alice Johnson', 1, 1, 2, 1599.98, '2025-01-15'),
('John Doe', 9, 2, 1, 5.99, '2025-01-20'),
('Maria Lopez', 13, 3, 1, 199.99, '2025-01-22'),
('Emily White', 2, 1, 1, 999.99, '2025-01-30'),

-- Sales from February
('Michael Brown', 10, 2, 2, 6.98, '2025-02-05'),
('Chris Adams', 14, 3, 1, 299.99, '2025-02-10'),
('Sophia Green', 20, 4, 1, 29.99, '2025-02-15'),
('David Clark', 3, 1, 1, 249.99, '2025-02-22'),

-- Sales from March
('Jessica Wilson', 15, 3, 1, 499.99, '2025-03-05'),
('Daniel Martinez', 5, 1, 1, 89.99, '2025-03-10'),
('Laura Scott', 7, 1, 3, 29.99, '2025-03-18'),
('Ethan Hall', 19, 4, 1, 39.99, '2025-03-22'),

-- Additional Transactions (More Customers & Random Dates)
('Linda Parker', 8, 1, 1, 19.99, '2025-01-08'),
('Robert Evans', 16, 3, 1, 129.99, '2025-02-03'),
('Olivia King', 22, 4, 1, 79.99, '2025-03-12'),
('Benjamin Nelson', 11, 2, 1, 2.99, '2025-01-25'),
('Matthew Lewis', 12, 2, 1, 14.99, '2025-02-28'),
('Sara Ramirez', 6, 1, 2, 19.99, '2025-03-15'),
('Anthony Harris', 4, 1, 1, 149.99, '2025-03-29');

3. Retrieve Sales Data
To get sales from the last 3 months, use:
SELECT customer_name, product_id, store_id, quantity, total_price, sale_date
FROM sales
WHERE sale_date >= DATE_SUB(CURRENT_DATE, INTERVAL 3 MONTH)
ORDER BY sale_date DESC;

### Generate report on top selling products
1. Get Top-Selling Products (By Quantity Sold)
SELECT p.name, SUM(s.quantity) AS total_sold
FROM sales s
JOIN products p ON s.product_id = p.product_id
GROUP BY p.product_id
ORDER BY total_sold DESC
LIMIT 10;

✅ Ranks products by total quantity sold
✅ Displays the top 10 selling products

2. Get Best-Selling Products (By Total Revenue)
SELECT p.name, SUM(s.total_price) AS total_revenue
FROM sales s
JOIN products p ON s.product_id = p.product_id
GROUP BY p.product_id
ORDER BY total_revenue DESC
LIMIT 10;

3. Sales Breakdown by Store
SELECT sl.store_name, p.name, SUM(s.quantity) AS total_sold, SUM(s.total_price) AS total_revenue
FROM sales s
JOIN products p ON s.product_id = p.product_id
JOIN store_locations sl ON s.store_id = sl.store_id
GROUP BY sl.store_id, p.product_id
ORDER BY total_sold DESC;

✅ Shows top-selling products at each store
✅ Useful for tracking performance across different location

###generate a Top-Selling Stores Report
1. Get Stores Ranked by Total Sales (Revenue)
SELECT sl.store_name, SUM(s.total_price) AS total_revenue
FROM sales s
JOIN store_locations sl ON s.store_id = sl.store_id
GROUP BY sl.store_id
ORDER BY total_revenue DESC
LIMIT 5;

2. Get Stores Ranked by Total Items Sold
SELECT sl.store_name, SUM(s.quantity) AS total_items_sold
FROM sales s
JOIN store_locations sl ON s.store_id = sl.store_id
GROUP BY sl.store_id
ORDER BY total_items_sold DESC
LIMIT 5;

### query the database to get total sales per products and another query for top per store
1. Get Total Sales Per Product
This query calculates total revenue and quantity sold per product:
SELECT p.name, SUM(s.quantity) AS total_quantity_sold, SUM(s.total_price) AS total_revenue
FROM sales s
JOIN products p ON s.product_id = p.product_id
GROUP BY p.product_id
ORDER BY total_quantity_sold DESC;
✅ Shows total units sold & revenue for each product
✅ Ranks them in descending order by quantity sold

2. Get Top-Selling Stores (By Total Revenue)
SELECT sl.store_name, SUM(s.total_price) AS total_revenue
FROM sales s
JOIN store_locations sl ON s.store_id = sl.store_id
GROUP BY sl.store_id
ORDER BY total_revenue DESC;
✅ Ranks stores based on total sales revenue
✅ Displays which store generated the most money

###nested query (subquery), here’s an example for getting top-selling products based on revenue:

SELECT name, total_revenue 
FROM (
    SELECT p.name, SUM(s.total_price) AS total_revenue
    FROM sales s
    JOIN products p ON s.product_id = p.product_id
    GROUP BY p.product_id
    ORDER BY total_revenue DESC
) AS top_products
LIMIT 5;

### a nested query for specific inventory analysis  
1. Get Products Below Average Stock Level
SELECT product_id, name, stock_quantity 
FROM products 
WHERE stock_quantity < (
    SELECT AVG(stock_quantity) FROM products
);

2. Get Stores With Less Than 10 Units of Any Product
SELECT store_id, store_name 
FROM store_locations 
WHERE store_id IN (
    SELECT store_id FROM store_inventory WHERE stock_quantity < 10
);

### generate alert system and stock replenishment suggestions using nested queries.
1. Automatic Low Stock Alerts
To identify products running low across stores, you can use:
SELECT p.name, si.store_id, si.stock_quantity
FROM store_inventory si
JOIN products p ON si.product_id = p.product_id
WHERE si.stock_quantity < (
    SELECT AVG(stock_quantity) FROM store_inventory
)
ORDER BY si.stock_quantity ASC;
✅ Subquery (SELECT AVG(stock_quantity) FROM store_inventory) calculates average stock level
✅ Main query fetches products with stock below average, sorted from lowest to highest

2. Recommend Restocking Based on Minimum Stock Level
SELECT product_id, store_id, (min_stock_level - stock_quantity) AS recommended_restock
FROM store_inventory
WHERE stock_quantity < min_stock_level;

3. Trigger Automatic Restock Requests
To auto-generate restock orders when stock falls below the minimum level:
CREATE TRIGGER auto_restock_trigger
AFTER UPDATE ON store_inventory
FOR EACH ROW
BEGIN
    IF NEW.stock_quantity < NEW.min_stock_level THEN
        INSERT INTO restock_requests (store_id, product_id, requested_quantity)
        VALUES (NEW.store_id, NEW.product_id, (NEW.min_stock_level - NEW.stock_quantity));
    END IF;
END;
✅ Automatically requests restocks when stock falls below the minimum threshold
✅ Eliminates the need for manual tracking
