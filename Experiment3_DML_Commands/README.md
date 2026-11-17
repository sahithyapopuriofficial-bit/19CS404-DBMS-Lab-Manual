# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
<img width="843" height="445" alt="image" src="https://github.com/user-attachments/assets/1530bf04-90a7-458d-83f7-066a7941a0c6" />


```
SELECT customer_id,cust_name,city,grade,salesman_id FROM customer WHERE grade IS NULL;
```

**Output:**

<img width="651" height="847" alt="image" src="https://github.com/user-attachments/assets/33051eab-8985-4fdc-940a-4db449239731" />


**Question 2**
---
<img width="830" height="317" alt="Screenshot 2026-11-17 114159" src="https://github.com/user-attachments/assets/6d61cd3e-3ce0-4751-a8bd-0131d41e52fd" />



```
SELECT customer_id,cust_name,city,grade,salesman_id FROM customer WHERE city='London' and grade>200;
```

**Output:**

<img width="862" height="825" alt="image" src="https://github.com/user-attachments/assets/6c4acb15-c95b-4469-b9f9-564cd90e5cf5" />


**Question 3**
---
<img width="527" height="406" alt="image" src="https://github.com/user-attachments/assets/9f7e92bd-159c-432c-bb32-b59609436957" />


```
SELECT patient_id,first_name,admission_date,discharge_date FROM Patients WHERE admission_date=discharge_date;
```

**Output:**

<img width="933" height="801" alt="image" src="https://github.com/user-attachments/assets/276721bd-c1df-4805-bd01-cdebf1f4640d" />


**Question 4**
---
<img width="631" height="378" alt="image" src="https://github.com/user-attachments/assets/4f5fb46e-1658-4d44-a5ae-36d78c10e4d3" />


```
SELECT * FROM EmployeePosition ORDER BY SALARY DESC LIMIT 3;
```

**Output:**

<img width="1088" height="822" alt="image" src="https://github.com/user-attachments/assets/310badfe-5fc8-48a2-bc1f-5ecb0940f523" />


**Question 5**
---
<img width="967" height="548" alt="image" src="https://github.com/user-attachments/assets/99e637b2-efac-4b96-9e79-a0020a225b28" />


```
SELECT customer_id,cust_name,city,grade,salesman_id FROM customer WHERE city<>'New York' AND grade=100;
```

**Output:**

<img width="645" height="851" alt="image" src="https://github.com/user-attachments/assets/75d279d1-d4ec-44a4-8c79-b05077c40321" />


**Question 6**
---
<img width="836" height="450" alt="image" src="https://github.com/user-attachments/assets/22adec6e-7d5c-4e3f-80d6-1ac724bb57c8" />


```
DELETE FROM customer WHERE (GRADE='3' OR AGENT_CODE='A008') AND (OUTSTANDING_AMT<5000);
```

**Output:**

<img width="557" height="806" alt="image" src="https://github.com/user-attachments/assets/19576c7f-4887-465a-acf4-5fac53b063a5" />


**Question 7**
---
<img width="847" height="452" alt="image" src="https://github.com/user-attachments/assets/8bbf2826-e1f0-4e00-a359-6acb23966300" />


```
DELETE FROM Customer WHERE GRADE=2 AND CUST_NAME LIKE 'M%' AND PAYMENT_AMT<3000;
```

**Output:**

<img width="561" height="805" alt="image" src="https://github.com/user-attachments/assets/7ddf4884-be98-435b-9d50-ce900bea0090" />


**Question 8**
---
<img width="717" height="212" alt="image" src="https://github.com/user-attachments/assets/0c695f6c-4323-4d5d-9489-909fa2322af6" />


```
UPDATE suppliers SET supplier_name='A1 Suppliers' WHERE supplier_id=8;
```

**Output:**

<img width="620" height="805" alt="image" src="https://github.com/user-attachments/assets/9b67bc15-7d9d-469b-ac31-95b42486075e" />


**Question 9**
---
<img width="717" height="236" alt="image" src="https://github.com/user-attachments/assets/057b17cb-4b03-4248-b17c-75cfbfdda898" />


```
UPDATE products SET product_name='Premium Bread' WHERE product_id=5;

```

**Output:**

<img width="851" height="850" alt="image" src="https://github.com/user-attachments/assets/95767dec-75f6-42b4-b0de-aaebb4d9c93b" />


**Question 10**
---
<img width="680" height="387" alt="image" src="https://github.com/user-attachments/assets/cb8ce45b-5c1c-4ece-89e5-ec8708505a39" />


```
UPDATE products SET reorder_lvl=40 WHERE category='Grocery';
```

**Output:**

<img width="425" height="690" alt="image" src="https://github.com/user-attachments/assets/8aae335f-e304-4c84-91c5-fea039187f9f" />

### MODULE COMPLETION SCREENSHOT
<img width="1917" height="900" alt="image" src="https://github.com/user-attachments/assets/43354d6d-00a0-4dc0-a435-4a87b5b9c0d1" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
