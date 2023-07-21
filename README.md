# assessment2
Sure! Below is the SQL code for creating the database schema and an explanation of each table:

```sql
-- Product table
CREATE TABLE Product (
    product_id INT PRIMARY KEY,
    name VARCHAR(100),
    description VARCHAR(255),
    price DECIMAL(10, 2),
    category VARCHAR(50)
);

-- Region table
CREATE TABLE Region (
    region_id INT PRIMARY KEY,
    name VARCHAR(100)
);

-- Time period table
CREATE TABLE TimePeriod (
    time_period_id INT PRIMARY KEY,
    name VARCHAR(50)
);

-- Customer table
CREATE TABLE Customer (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    address VARCHAR(255),
    age INT,
    loyalty_status VARCHAR(50)
);

-- Purchase table
CREATE TABLE Purchase (
    purchase_id INT PRIMARY KEY,
    customer_id INT,
    time_period_id INT,
    total_purchase_amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES Customer(customer_id),
    FOREIGN KEY (time_period_id) REFERENCES TimePeriod(time_period_id)
);

-- Purchase product table (junction table)
CREATE TABLE PurchaseProduct (
    purchase_id INT,
    product_id INT,
    PRIMARY KEY (purchase_id, product_id),
    FOREIGN KEY (purchase_id) REFERENCES Purchase(purchase_id),
    FOREIGN KEY (product_id) REFERENCES Product(product_id)
);

-- Product region table (junction table)
CREATE TABLE ProductRegion (
    product_id INT,
    region_id INT,
    PRIMARY KEY (product_id, region_id),
    FOREIGN KEY (product_id) REFERENCES Product(product_id),
    FOREIGN KEY (region_id) REFERENCES Region(region_id)
);

-- Inventory table
CREATE TABLE Inventory (
    inventory_id INT PRIMARY KEY,
    product_id INT,
    stock_level INT,
    FOREIGN KEY (product_id) REFERENCES Product(product_id)
);
```

Explanation:
- The `Product` table stores information about products. It has attributes like `product_id` (unique identifier for the product), `name`, `description`, `price`, and `category`.
- The `Region` table stores information about regions where products are sold. It has attributes like `region_id` (unique identifier for the region) and `name`.
- The `TimePeriod` table stores information about different time periods, such as quarters or months. It has attributes like `time_period_id` (unique identifier for the time period) and `name`.
- The `Customer` table stores information about customers. It has attributes like `customer_id` (unique identifier for the customer), `name`, `address`, `age`, and `loyalty_status`.
- The `Purchase` table stores information about each purchase made by customers. It has attributes like `purchase_id` (unique identifier for the purchase), `customer_id` (foreign key referencing `Customer` table), `time_period_id` (foreign key referencing `TimePeriod` table), and `total_purchase_amount`.
- The `PurchaseProduct` table is a junction table representing the many-to-many relationship between purchases and products. It has attributes `purchase_id` (foreign key referencing `Purchase` table) and `product_id` (foreign key referencing `Product` table).
- The `ProductRegion` table is another junction table representing the many-to-many relationship between products and regions. It has attributes `product_id` (foreign key referencing `Product` table) and `region_id` (foreign key referencing `Region` table).
- The `Inventory` table stores information about the stock level of each product. It has attributes like `inventory_id` (unique identifier for the inventory entry), `product_id` (foreign key referencing `Product` table), and `stock_level`.

By creating this database schema, the company can now effectively track its sales data, customer data, and inventory data using SQL database. The relationships between the tables allow for efficient data management and retrieval, enabling the company to make informed decisions about its business operations.
