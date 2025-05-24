# Database-Design-for-a-Local-Pizza-Business
# 🍕 Helena Pizzeria Database

This project contains the relational database schema and documentation for Helena Pizzeria's business operations. The database is designed to manage orders, menu items, customers, inventory, staff scheduling, and deliveries with scalability and clarity.

## 📂 Project Contents

- `schema.sql` - SQL statements for creating the database tables with correct primary and foreign keys.
- `STAKEHOLDER_REQUIREMENTS.md` - Business requirements, stakeholder needs, and design rationale.
- `README.md` - Project overview and setup guide.
- `ERD.png` (optional) - Entity-Relationship Diagram for visual reference.

## 🧑‍💼 Purpose

The goal of this database is to support Helena Pizzeria in managing its end-to-end operations:
- Handling customer orders (delivery or dine-in)
- Tracking ingredients and recipes
- Managing inventory
- Scheduling staff
- Storing customer and delivery data

## 🛠️ Technologies Used

- SQL (PostgreSQL / MySQL compatible)
- Markdown for documentation
- Optional: dbdiagram.io or Draw.io for ERD

## 🧱 Features

- Comprehensive ERD covering orders, customers, recipes, ingredients, and staff
- Foreign key constraints for referential integrity
- Ready-to-use SQL DDL for creating all tables

## 📦 Tables Included

- `orders`
- `customers`
- `address`
- `item`
- `recipe`
- `inventory`
- `ingredient`
- `rota`
- `staff`

## 🛠️ Getting Started

### Prerequisites

- MySQL Server (5.7+ or 8.0+)
- MySQL Workbench or any compatible SQL client

### Setup Instructions

1. Clone this repository to your local machine.
2. Open your MySQL interface.
3. Create a new database:
   ```sql
   CREATE DATABASE helena_pizzeria;
   USE helena_pizzeria;
4. Execute the SQL script below to create and link all tables with proper constraints.
   Copy and paste the SQL code below into your MySQL environment:

   CREATE TABLE `orders` (
    `order_id` varchar(10)  NOT NULL ,
    `created_at` datetime  NOT NULL ,
    `item_id` varchar(10)  NOT NULL ,
    `quantity` int  NOT NULL ,
    `cst_id` int  NOT NULL ,
    `delivery` boolean  NOT NULL ,
    `address_id` int  NOT NULL ,
    PRIMARY KEY (
        `order_id`
    )
);

CREATE TABLE `customers` (
    `cst_id` int  NOT NULL ,
    `cst_firstname` vachar(100)  NOT NULL ,
    `cst_lastname` vachar(100)  NOT NULL ,
    PRIMARY KEY (
        `cst_id`
    )
);

CREATE TABLE `address` (
    `address_id` int  NOT NULL ,
    `delivery_address1` varchar(200)  NOT NULL ,
    `delivery_address2` Varchar(200)  NULL ,
    `delivery_city` varchar(50)  NOT NULL ,
    `delivery_zipcode` varchar(20)  NOT NULL ,
    PRIMARY KEY (
        `address_id`
    )
);

CREATE TABLE `item` (
    `item_id` varchar(10)  NOT NULL ,
    `sku` varchar(20)  NOT NULL ,
    `item_name` varchar(20)  NOT NULL ,
    `item_category` varchar(100)  NOT NULL ,
    `item_size` varchar(10)  NOT NULL ,
    `item_prize` decimal(10,2)  NOT NULL ,
    PRIMARY KEY (
        `item_id`
    )
);

CREATE TABLE `recipe` (
    `recipe_id` varchar(20)  NOT NULL ,
    `ing_id` varchar(10)  NOT NULL ,
    `quantity` int  NOT NULL ,
    PRIMARY KEY (
        `recipe_id`
    )
);

CREATE TABLE `inventory` (
    `inv_id` int  NOT NULL ,
    `item_id` varchar(10)  NOT NULL ,
    `quantity` int  NOT NULL ,
    PRIMARY KEY (
        `inv_id`
    )
);

CREATE TABLE `ingredient` (
    `ing_id` varchar(10)  NOT NULL ,
    `ing_name` varchar(205)  NOT NULL ,
    `ing_weight` int  NOT NULL ,
    `ing_meas` varchar(20)  NOT NULL ,
    `ing_price` decimal(5,2)  NOT NULL ,
    PRIMARY KEY (
        `ing_id`
    )
);

CREATE TABLE `rota` (
    `rota_id` varchar(20)  NOT NULL ,
    `date` datetime  NOT NULL ,
    `shift_id` varchar(20)  NOT NULL ,
    `staff_id` varchar(20)  NOT NULL ,
    PRIMARY KEY (
        `rota_id`
    )
);

CREATE TABLE `Staff` (
    `staff_id` int  NOT NULL ,
    `first_name` varchar(100)  NOT NULL ,
    `last_name` varchar(100)  NOT NULL ,
    `position` varchar(100)  NOT NULL ,
    `hourly_rate` decimal(5,2)  NOT NULL ,
    PRIMARY KEY (
        `staff_id`
    )
);

ALTER TABLE `orders` ADD CONSTRAINT `fk_orders_item_id` FOREIGN KEY(`item_id`)
REFERENCES `item` (`item_id`);

ALTER TABLE `orders` ADD CONSTRAINT `fk_orders_cst_id` FOREIGN KEY(`cst_id`)
REFERENCES `customers` (`cst_id`);

ALTER TABLE `address` ADD CONSTRAINT `fk_address_address_id` FOREIGN KEY(`address_id`)
REFERENCES `orders` (`address_id`);

ALTER TABLE `item` ADD CONSTRAINT `fk_item_sku` FOREIGN KEY(`sku`)
REFERENCES `recipe` (`recipe_id`);

ALTER TABLE `recipe` ADD CONSTRAINT `fk_recipe_ing_id` FOREIGN KEY(`ing_id`)
REFERENCES `inventory` (`item_id`);

ALTER TABLE `ingredient` ADD CONSTRAINT `fk_ingredient_ing_id` FOREIGN KEY(`ing_id`)
REFERENCES `recipe` (`ing_id`);

ALTER TABLE `rota` ADD CONSTRAINT `fk_rota_date` FOREIGN KEY(`date`)
REFERENCES `orders` (`created_at`);

ALTER TABLE `Staff` ADD CONSTRAINT `fk_Staff_staff_id` FOREIGN KEY(`staff_id`)
REFERENCES `rota` (`staff_id`);





