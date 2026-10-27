# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Write an SQL query to change the name of the column id to employee_id in the table employee.

```
ALTER TABLE employee RENAME COLUMN id TO employee_id;
```

**Output:**

<img width="631" height="795" alt="image" src="https://github.com/user-attachments/assets/7c2c8264-a846-4b6e-92ad-44747573dbb5" />



**Question 2**
---
Insert all products from Discontinued_products into Products.
Table attributes are ProductID, ProductName, Price, Stock

```
INSERT INTO Products(ProductID,ProductName,Price,Stock)SELECT ProductID,ProductName,Price,Stock FROM Discontinued_products;
```

**Output:**

<img width="681" height="787" alt="image" src="https://github.com/user-attachments/assets/1607d2bf-89c5-480b-b365-6df55a06d6d1" />


**Question 3**
---
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

```
INSERT INTO Student_details(RollNo,Name,Gender,Subject,Marks)values(201,"David Lee","M","Physics",92);
```

**Output:**

<img width="771" height="801" alt="image" src="https://github.com/user-attachments/assets/63cec9e5-0764-4a4b-b058-2f62b24a655c" />


**Question 4**
---
Create a new table named item with the following specifications and constraints:
1. item_id as TEXT and as primary key.
2. item_desc as TEXT.
3. rate as INTEGER.
4. icom_id as TEXT with a length of 4.
5. icom_id is a foreign key referencing com_id in the company table.
6. The foreign key should cascade updates and deletes.
7. item_desc and rate should not accept NULL.

```
CREATE TABLE item(item_id TEXT primary key,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT check(length<=4),
foreign key(icom_id) references company(com_id) ON UPDATE CASCADE SET NULL,
foreign key(icom_id) references company(com_id) ON DELETE SET NULL);
```

**Output:**

<img width="567" height="795" alt="image" src="https://github.com/user-attachments/assets/b5d89d0f-ced5-4930-8b8d-d6a1146f0054" />


**Question 5**
---
Create a table named Products with the following constraints:
ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

```sql
CREATE TABLE Products(ProductID int primary key,
ProductName text NOT NULL,
Price real check(Price>=0),
Stock int check(Stock>=0));
```

**Output:**

<img width="687" height="771" alt="image" src="https://github.com/user-attachments/assets/cf0ad91d-2411-406d-be88-3fa3288df90f" />


**Question 6**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```
Create table Shipments(ShipmentID int primary key,
ShipmentDate date,
SupplierID int,
OrderID int,
foreign key(SupplierID) references Suppliers(SupplierID),
foreign key(OrderID) references Orders(OrderID));
```

**Output:**

<img width="765" height="845" alt="image" src="https://github.com/user-attachments/assets/6a2f2725-f834-4d6a-a0c8-e612730f48e1" />


**Question 7**
---
Create a table named Reviews with the following columns:
ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```
Create a table named Reviews with the following columns:
ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
```

**Output:**

<img width="565" height="791" alt="image" src="https://github.com/user-attachments/assets/8c6738e9-07e6-4e90-8989-fc010a1ae502" />


**Question 8**
---
Insert the following employees into the Employee table:
EmployeeID  Name   Position    Department  Salary
2           John Smith  Developer   IT     75000    
3           Anna Bell   Designer    Marketing 68000


```
insert into Employee(EmployeeID,Name,Position,Department,Salary)values(2,"John Smith","Developer","IT",75000),
(3,"Anna Bell","Designer","Marketing",68000);
```

**Output:**

<img width="641" height="826" alt="image" src="https://github.com/user-attachments/assets/7533a85a-531c-47e7-af53-8cee663632df" />


**Question 9**
---
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0

```
Create table products(product_id int primary key,
product_name text NOT NULL,
list_price DECIMAL(10,2) NOT NULL check(list_price>=discount),
discount DECIMAL(10,2) NOT NULL DEFAULT 0 check(discount>=0),
check(list_price>=0));
```

**Output:**

<img width="570" height="773" alt="image" src="https://github.com/user-attachments/assets/b121297c-8ca6-4dce-8028-4a8960c75f3b" />


**Question 10**
---
Write an SQL command can to add a column named email of type TEXT to the customers table

```
ALTER TABLE customers ADD email TEXT;
```

**Output:**

<img width="685" height="822" alt="image" src="https://github.com/user-attachments/assets/9265ed35-f0ed-4631-bf72-da2ef46c5a86" />

## SCREENSHOT OF MODULE 1 COMPLETION
<img width="341" height="170" alt="image" src="https://github.com/user-attachments/assets/68f185ed-0aa8-4c47-bbaa-a618675b9e6d" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
