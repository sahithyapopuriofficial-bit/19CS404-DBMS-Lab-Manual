# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

### PL/SQL Query
```
CREATE TABLE employee1 (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);

CREATE TABLE employee_log (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    log_date DATE
);

CREATE OR REPLACE TRIGGER trg_employee_insert
AFTER INSERT ON employee1
FOR EACH ROW
BEGIN
    INSERT INTO employee_log
    VALUES (
        :NEW.emp_id,
        :NEW.emp_name,
        :NEW.designation,
        SYSDATE
    );
END;


INSERT INTO employee1
VALUES (1, 'Ravi', 'Manager');

SELECT * FROM employee_log;
```
**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

<img width="690" height="641" alt="image" src="https://github.com/user-attachments/assets/462374f0-28f5-4396-91c5-4cadf716838b" />
<img width="865" height="235" alt="image" src="https://github.com/user-attachments/assets/5c2f4e50-0c72-40e3-91ec-811f1d811805" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

### PL/SQL Query
```
CREATE TABLE sensitive_data (
    id NUMBER PRIMARY KEY,
    data VARCHAR2(100)
);

INSERT INTO sensitive_data VALUES (1, 'Confidential Information');

CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(
        -20001,
        'ERROR: Deletion not allowed on this table.'
    );
END;


DELETE FROM sensitive_data WHERE id = 1;
```
**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`
<img width="696" height="597" alt="image" src="https://github.com/user-attachments/assets/59482304-b8cd-4c9d-a635-07adb3ce4cdb" />
<img width="796" height="163" alt="image" src="https://github.com/user-attachments/assets/c1311ba4-c8ca-4c9d-86df-35482c40c092" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

### PL/SQL Query
```
CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(50),
    price NUMBER(10,2)
);

ALTER TABLE products ADD last_modified TIMESTAMP;

INSERT INTO products VALUES (1, 'Laptop', 50000, NULL);

CREATE OR REPLACE TRIGGER trg_update_timestamp
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;


UPDATE products
SET price = 55000
WHERE product_id = 1;

SELECT * FROM products;
```
**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.
<img width="688" height="542" alt="image" src="https://github.com/user-attachments/assets/a57f7173-7e01-4099-beaa-139e73ca67b8" />
<img width="856" height="226" alt="image" src="https://github.com/user-attachments/assets/6aa04a99-2092-4616-89bf-56ba8b15d2b7" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

### PL/SQL Query
```
CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(50),
    amount NUMBER(10,2)
);

CREATE TABLE audit_log (
    update_count NUMBER
);

INSERT INTO audit_log VALUES (0);

INSERT INTO customer_orders VALUES (1, 'Ravi', 5000);

CREATE OR REPLACE TRIGGER trg_update_count
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;


UPDATE customer_orders
SET amount = 6000
WHERE order_id = 1;

SELECT * FROM audit_log;
```
**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
<img width="688" height="565" alt="Screenshot 2026-11-17 211958" src="https://github.com/user-attachments/assets/0d154db3-596b-4e58-8b3e-04684dcf085e" />
<img width="728" height="210" alt="Screenshot 2026-11-17 212130" src="https://github.com/user-attachments/assets/c5917d07-8c30-4ee1-8d55-7f258b5d8f68" />


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

### PL/SQL Query
```
CREATE TABLE employee2 (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON employee2
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20001,
            'ERROR: Salary below minimum threshold.'
        );
    END IF;
END;

INSERT INTO employee2 VALUES (1, 'Ravi', 5000);

INSERT INTO employee2 VALUES (2, 'Priya', 2500);
```
**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`
<img width="703" height="643" alt="image" src="https://github.com/user-attachments/assets/b8b8b112-1711-4489-9573-0d74fa6060ad" />
<img width="937" height="167" alt="image" src="https://github.com/user-attachments/assets/0712c2b2-8f6d-4a6b-9011-e4d405a45f46" />

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
