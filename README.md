# 🍕 Helena Pizzeria Database Schema

This repository contains the SQL schema for Helena Pizzeria, a restaurant database designed to manage orders, inventory, customers, staff scheduling, and menu items.

## 📌 Overview

This schema supports:
- Customer order management
- Menu item and recipe tracking
- Inventory of ingredients
- Staff rota scheduling
- Delivery address handling

The database ensures data integrity through well-defined primary and foreign key constraints.

---

## 🚀 How to Use

To use this database schema:

1. **Install MySQL**  
   Ensure MySQL Server is installed and running on your system.

2. **Create a New Database**
   ```sql
   CREATE DATABASE helena_pizzeria;
   USE helena_pizzeria;
   ```

3. **Execute the SQL Script**  
   Copy and run the following SQL code to create all tables and relationships:


```sql
CREATE TABLE `orders` (
    `order_id` varchar(10)  NOT NULL ,
    `created_at` datetime  NOT NULL ,
    `item_id` varchar(10)  NOT NULL ,
    `quantity` int  NOT NULL ,
    `cst_id` int  NOT NULL ,
    `delivery` boolean  NOT NULL ,
    `address_id` int  NOT NULL ,
    PRIMARY KEY (`order_id`)
);

CREATE TABLE `customers` (
    `cst_id` int  NOT NULL ,
    `cst_firstname` vachar(100)  NOT NULL ,
    `cst_lastname` vachar(100)  NOT NULL ,
    PRIMARY KEY (`cst_id`)
);

CREATE TABLE `address` (
    `address_id` int  NOT NULL ,
    `delivery_address1` varchar(200)  NOT NULL ,
    `delivery_address2` Varchar(200)  NULL ,
    `delivery_city` varchar(50)  NOT NULL ,
    `delivery_zipcode` varchar(20)  NOT NULL ,
    PRIMARY KEY (`address_id`)
);

CREATE TABLE `item` (
    `item_id` varchar(10)  NOT NULL ,
    `sku` varchar(20)  NOT NULL ,
    `item_name` varchar(20)  NOT NULL ,
    `item_category` varchar(100)  NOT NULL ,
    `item_size` varchar(10)  NOT NULL ,
    `item_prize` decimal(10,2)  NOT NULL ,
    PRIMARY KEY (`item_id`)
);

CREATE TABLE `recipe` (
    `recipe_id` varchar(20)  NOT NULL ,
    `ing_id` varchar(10)  NOT NULL ,
    `quantity` int  NOT NULL ,
    PRIMARY KEY (`recipe_id`)
);

CREATE TABLE `inventory` (
    `inv_id` int  NOT NULL ,
    `item_id` varchar(10)  NOT NULL ,
    `quantity` int  NOT NULL ,
    PRIMARY KEY (`inv_id`)
);

CREATE TABLE `ingredient` (
    `ing_id` varchar(10)  NOT NULL ,
    `ing_name` varchar(205)  NOT NULL ,
    `ing_weight` int  NOT NULL ,
    `ing_meas` varchar(20)  NOT NULL ,
    `ing_price` decimal(5,2)  NOT NULL ,
    PRIMARY KEY (`ing_id`)
);

CREATE TABLE `rota` (
    `rota_id` varchar(20)  NOT NULL ,
    `date` datetime  NOT NULL ,
    `shift_id` varchar(20)  NOT NULL ,
    `staff_id` varchar(20)  NOT NULL ,
    PRIMARY KEY (`rota_id`)
);

CREATE TABLE `Staff` (
    `staff_id` int  NOT NULL ,
    `first_name` varchar(100)  NOT NULL ,
    `last_name` varchar(100)  NOT NULL ,
    `position` varchar(100)  NOT NULL ,
    `hourly_rate` decimal(5,2)  NOT NULL ,
    PRIMARY KEY (`staff_id`)
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
```


---

## 🧠 Entity Summary

| Table        | Purpose                                 |
|--------------|------------------------------------------|
| `orders`     | Tracks customer orders and delivery info |
| `customers`  | Stores customer names                    |
| `address`    | Stores delivery addresses                |
| `item`       | Menu items for sale                      |
| `recipe`     | Recipe structure for each item           |
| `inventory`  | Tracks ingredient quantities in stock    |
| `ingredient` | Ingredient details and cost              |
| `rota`       | Staff scheduling                         |
| `staff`      | Staff profiles and wage info             |

---

## 📊 ER Diagram

An [Entity Relationship Diagram (ERD)](./AEntity_Relationship_Diagram_(ERD)_for_a_database_.png) is included in this repo to visualize the relationships between tables.

---

## 📝 Notes

- All primary and foreign key constraints are included for referential integrity.
- Table and column names follow consistent naming conventions.
- Designed for scalability (future support for payments, feedback, etc.)

---

## 🙋 Author

Built by Helena Pizzeria Ops for learning, internal use, and demo purposes.

---

## 📃 License

This project is licensed under the MIT License. Use and modify freely.
