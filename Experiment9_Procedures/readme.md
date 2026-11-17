# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

### PL/SQL Query
```
CREATE OR REPLACE PROCEDURE find_square(n IN NUMBER)
IS
    sq NUMBER;
BEGIN
    sq := n * n;
    DBMS_OUTPUT.PUT_LINE('Square of ' || n || ' is ' || sq);
END;


BEGIN
    find_square(6);
END;
```
**Expected Output:**  
Square of 6 is 36

<img width="692" height="572" alt="image" src="https://github.com/user-attachments/assets/2a16cb66-176f-4750-ba4e-963643ef864d" />
<img width="407" height="228" alt="image" src="https://github.com/user-attachments/assets/d8887fcd-dff8-43d6-8fa2-d96642e55d44" />


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

### PL/SQL Query
```
CREATE OR REPLACE FUNCTION get_factorial(n IN NUMBER)
RETURN NUMBER
IS
    fact NUMBER := 1;
BEGIN
    FOR i IN 1..n LOOP
        fact := fact * i;
    END LOOP;

    RETURN fact;
END;

BEGIN
    DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || get_factorial(5));
END;
```
**Expected Output:**  
Factorial of 5 is 120

<img width="702" height="638" alt="image" src="https://github.com/user-attachments/assets/dbc19161-b907-466a-81c8-70ec96065c31" />
<img width="625" height="225" alt="image" src="https://github.com/user-attachments/assets/e241239e-9095-420d-be64-fe14fb285a0c" />


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

### PL/SQL Query
```
CREATE OR REPLACE PROCEDURE check_even_odd(n IN NUMBER)
IS
BEGIN
    IF MOD(n, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(n || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(n || ' is Odd');
    END IF;
END;


BEGIN
    check_even_odd(12);
END;
```
**Expected Output:**  
12 is Even

<img width="701" height="607" alt="image" src="https://github.com/user-attachments/assets/77b87d06-ba56-41dc-9607-98f911baeb35" />
<img width="397" height="235" alt="image" src="https://github.com/user-attachments/assets/8c2ec0fc-c6a5-4eab-9e25-41a6c214fe0b" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

### PL/SQL Query
```
CREATE OR REPLACE FUNCTION reverse_number(n IN NUMBER)
RETURN NUMBER
IS
    num NUMBER := n;
    rev NUMBER := 0;
    rem NUMBER;
BEGIN
    WHILE num > 0 LOOP
        rem := MOD(num, 10);
        rev := rev * 10 + rem;
        num := TRUNC(num / 10);
    END LOOP;

    RETURN rev;
END;


BEGIN
    DBMS_OUTPUT.PUT_LINE(
        'Reversed number of 1234 is ' || reverse_number(1234)
    );
END;
```
**Expected Output:**  
Reversed number of 1234 is 4321

<img width="688" height="708" alt="image" src="https://github.com/user-attachments/assets/d6bb6224-1998-4f58-a4e5-c431be78279a" />
<img width="573" height="267" alt="image" src="https://github.com/user-attachments/assets/9efb1a75-049f-49fd-84de-3bfb33bef00d" />

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

### PL/SQL Query
```
CREATE OR REPLACE PROCEDURE print_table(n IN NUMBER)
IS
BEGIN
    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(n || ' x ' || i || ' = ' || (n * i));
    END LOOP;
END;

BEGIN
    print_table(5);
END;
```
**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

<img width="697" height="568" alt="image" src="https://github.com/user-attachments/assets/063db46b-582d-40e3-b153-fc44b1ca6889" />
<img width="376" height="393" alt="image" src="https://github.com/user-attachments/assets/6310fbc7-411d-46a8-bfed-f7fa297fe920" />


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
