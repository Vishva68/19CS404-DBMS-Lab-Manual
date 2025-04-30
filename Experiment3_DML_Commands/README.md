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
-- Paste Question 1 here
```
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 
```sql
-- Paste your SQL code below for Question 1
Customer table (customer_id,cust_name,city,grade,salesman_id)
---
```
```
sql
-- UPDATE Customer
SET grade = 5
WHERE city = 'Chennai';
```

**Output:**

![Output1](output.png)
![Output1](output.png)![Screenshot 2025-04-29 235409](https://github.com/user-attachments/assets/d704ec17-9840-4fba-b073-03978adee9e5)


**Question 2**
---
-- Paste Question 2 here
-- 
```
Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.
SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
For example:
Test	Result
select changes();
changes()
----------
3
```sql
-- Paste your SQL code below for Question 2
```
```
sql
-- UPDATE SALES
SET total_sell_price = quantity * sell_price
WHERE product_id = 10;
```

**Output:**

![Output2](output.png)

![Output2](output.png)![Screenshot 2025-04-29 235446](https://github.com/user-attachments/assets/112e3e04-2002-4e42-a9b5-b38e8aff2e5a)


**Question 3**
---
-- Paste Question 3 here
```
Write a SQL statement to Increase the selling price per unit by 5% for product ID 15 who's sale is on '2023-01-31'.
```sql
-- Paste your SQL code below for Question 3
sales(sale_id,sale_date,product_id,quantity,sell_price,total_sell_price)
For example:
Test	Result
select changes();
changes()
----------
3
```
```
sql
-- UPDATE sales
SET sell_price = sell_price * 1.05
WHERE product_id = 15 AND sale_date = '2023-01-31';
```

**Output:**

![Output3](output.png)
![Output3](output.png)![Screenshot 2025-04-29 235504](https://github.com/user-attachments/assets/b99aa758-3329-4197-b127-9da1c14c7e26)


**Question 4**
---
-- Paste Question 4 here
```
For products with a profit % less than 30% of selling price, update the selling price to provide a profit margin of 35% over cost price of the product in the products table.
PRODUCTS TABLE
name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
For example:
Test	Result
SELECT*FROM Products WHERE supplier_id = 10;
product_id  product_name      category    cost_price  sell_price  reorder_lvl  quantity    supplier_id
----------  ----------------  ----------  ----------  ----------  -----------  ----------  -----------
6           Detergent Powder  Snacks      60          80          20           40          10
7           Surf Excel Deter  Snacks      85          100         10           40          10
8           Detergent Ariel   Items       85          100         10           40          10
product_id  product_name      category    cost_price  sell_price  reorder_lvl  quantity    supplier_id
----------  ----------------  ----------  ----------  ----------  -----------  ----------  -----------
6           Detergent Powder  Snacks      60          81          20           40          10
7           Surf Excel Deter  Snacks      85          114         10           40          10
8           Detergent Ariel   Items       85          114         10           40          10
```sql
-- Paste your SQL code below for Question 4
```
```
sql
-- UPDATE Products
SET sell_price = ROUND(cost_price * 1.345)
WHERE (sell_price - cost_price) / sell_price < 1.34;
```

**Output:**

![Output4](output.png)
![Output4](output.png)![Screenshot 2025-04-29 235527](https://github.com/user-attachments/assets/11bb99e9-9eb3-4177-9189-fdf2ab376bcb)


**Question 5**
---
-- Paste Question 5 here
--
```
Write a SQL statement to Increase the salary by 500 and email as 'updated' for employees with job ID 'SA_REP' and commission percentage greater than 0.15
Employees table
---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:
Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, EMAIL, SALARY, JOB_ID FROM EMPLOYEES 
WHERE job_id = 'SA_REP' AND EMAIL='updated' LIMIT 5;
EMPLOYEE_ID  FIRST_NAME  EMAIL       SALARY      JOB_ID
-----------  ----------  ----------  ----------  ----------
150          Peter       updated     10500       SA_REP
151          David       updated     10000       SA_REP
152          Peter       updated     9500        SA_REP
153          Christophe  updated     8500        SA_REP
154          Nanette     updated     8000        SA_REP
```sql
-- Paste your SQL code below for Question 5
```
```
sql
--UPDATE Employees
SET salary = salary + 500,
    email = 'updated'
WHERE job_id = 'SA_REP' AND commission_pct > 0.15;
```

**Output:**

![Output5](output.png)
![Output5](output.png)![Screenshot 2025-04-29 235552](https://github.com/user-attachments/assets/be84a77a-e193-470b-aa65-4edf6a4204a6)


**Question 6**
---
-- Paste Question 6 here
-- 
```
Write a SQL query to Delete customers whose 'GRADE' is greater than 2 and have a 'PAYMENT_AMT' less than the average 'PAYMENT_AMT' for all customers, or whose 'OUTSTANDING_AMT' is greater than 8000:
Sample table: Customer
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:
Test	Result
select changes();
changes()
----------
12
```sql
-- Paste your SQL code below for Question 6
```
```
sql
-- DELETE FROM Customer
WHERE (grade > 2 AND payment_amt < (SELECT AVG(payment_amt) FROM Customer))
   OR outstanding_amt > 8000;
```

**Output:**

![Output6](output.png)
![Output6](output.png)![Screenshot 2025-04-29 235621](https://github.com/user-attachments/assets/e1bb8d26-827d-45b6-bc62-d449087e5d8a)


**Question 7**
---
-- Paste Question 7 here
 ```
Write a SQL query to Delete All Doctors with a NULL Last Name
Sample table: Doctors
attributes : doctor_id, first_name, last_name, specialization
For example:
Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin                   Cardiology
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
```sql
-- Paste your SQL code below for Question 7
```
```
sql
-- DELETE FROM Doctors
WHERE last_name IS NULL;
```

**Output:**

![Output7](output.png)
![Output7](output.png)![Screenshot 2025-04-29 235654](https://github.com/user-attachments/assets/86771390-aa17-42ff-9819-9629b94d576d)


**Question 8**
---
-- Paste Question 8 here
--
```
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'
Sample table: Doctors
attributes : doctor_id, first_name, last_name, specialization
```sql
-- Paste your SQL code below for Question 8
```
```
sql
-- DELETE FROM Doctors
WHERE specialization = 'Cardiology';
```

**Output:**

![Output8](output.png)
![Output8](output.png)![Screenshot 2025-04-29 235710](https://github.com/user-attachments/assets/3ba306ac-628c-4a1c-9576-0a53b55c780a)


**Question 9**
---
-- Paste Question 9 here
-- 
```
Write a SQL query to Delete a Specific Surgery whose ID is 3
Sample table: Surgeries
attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:
Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
```sql
-- Paste your SQL code below for Question 9
```
```
sql
-- DELETE FROM Surgeries
WHERE surgery_id = 3;
```

**Output:**

![Output9](output.png)
![Output9](output.png)![Screenshot 2025-04-29 235727](https://github.com/user-attachments/assets/c6ed26a7-d549-49e5-b114-dc368d8e2718)


**Question 10**
---
-- Paste Question 10 here
-- 
```
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is not equal to 3.
 
Sample table: Customer
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:
Test	Result
select distinct(grade)from customer;
GRADE
----------
2
3
1
0
GRADE
----------
3
```sql
-- Paste your SQL code below for Question 10
```
```
sql
-- DELETE FROM Customer
WHERE grade <> 3;
```

**Output:**

![Output10](output.png)
![Output10](output.png)![Screenshot 2025-04-29 235743](https://github.com/user-attachments/assets/28a36b18-5e2c-442c-b0ca-ecba34e9929d)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
