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
-- Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
For example:

Test	Result
pragma table_info('Reviews');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           ReviewID    INTEGER     0                       0
1           ProductID   INTEGER     0                       0
2           Rating      REAL        0                       0
3           ReviewText  TEXT        0                       0

```sql
--create table Reviews(
ReviewID INTEGER ,
ProductID INTEGER ,
Rating REAL,
ReviewText TEXT );
```

**Output:**

![Output1](output.png)![Screenshot 2025-04-28 142822](https://github.com/user-attachments/assets/3b71de17-a273-46da-8014-cccc4db61672)


**Question 2**
---
-- Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.

For example:

Test	Result
PRAGMA table_info(employee);
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           department  INTEGER     0                       0
3           manager_id  INTEGER     0           NULL        0

```sql
-- alter table employee
add column department_id INTEGER ;
alter table employee
add column manager_id INTEGER default NULL ;
```

**Output:**

![Output2](output.png)![Screenshot 2025-04-28 142846](https://github.com/user-attachments/assets/82f25e4e-a380-4f58-a7f1-c31cef8e85c2)


**Question 3**
---
-- Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
For example:

Test	Result
select * from student_details;
RollNo      Name           Gender      Subject     MARKS
----------  -------------  ----------  ----------  ----------
1           Alice Johnson  Female      Math        85
2           Bob Smith      Male        Science     90
3           Charlie Brown  Male        English     78

```sql
-- insert into student_details(RollNo,Name,Gender,Subject,MARKS)
select  RollNo,Name,Gender,Subject,MARKS from Archived_students ;
```

**Output:**

![Output3](output.png)![Screenshot 2025-04-28 142912](https://github.com/user-attachments/assets/190cb63b-07c4-42af-b53f-848ce1dc3194)


**Question 4**
---
-- Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName

```sql
-- create table Products(
ProductID INTEGER primary key ,
ProductName TEXT not null,
Price REAL check(price>0),
Stock INTEGER check(Stock>=0));
```

**Output:**

![Output4](output.png)![Screenshot 2025-04-28 142932](https://github.com/user-attachments/assets/a271dfd0-6df3-41e5-b6b2-befc4eb4dd6a)


**Question 5**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
 
For example:

Test	Result
SELECT CustomerID, Name, Address
FROM Customers;
CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St
```sql
-- insert into Customers (CustomerID,Name,Address)
values ("304","Peter Parker","Spider St");
```

**Output:**

![Output5](output.png)![Screenshot 2025-04-28 142955](https://github.com/user-attachments/assets/f056457f-91fb-4ea0-b3b6-405596abb993)


**Question 6**
---Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5
-- 

```sql
-- create table item(
item_id TEXT primary key,
item_desc TEXT not null,
rate INTEGER not null,
icom_id TEXT(4),
foreign key(icom_id)references company(com_id)
on update cascade
on delete cascade);
```

**Output:**

![Output6](output.png)![Screenshot 2025-04-28 143013](https://github.com/user-attachments/assets/16ed068e-7f56-4927-9e6a-4216103ee0bb)


**Question 7**
---
-- Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	Result
select * from Products;
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5

```sql
-- INSERT into products( ProductID,ProductName,Price,Stock)
SELECT  ProductID,ProductName,Price,Stock FROM Discontinued_products 
```

**Output:**

![Output7](output.png)![Screenshot 2025-04-28 143051](https://github.com/user-attachments/assets/689696b0-386e-470b-8fe5-7b44270afcf3)


**Question 8**
---
-- Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.

For example:

Test	Result
SELECT * FROM Employee WHERE EmployeeID = 001;
EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
1           Sarah Parker  Manager     HR          60000

```sql
-- INSERT into employee(EmployeeID,Name,Position,Department,Salary) 
values("1","Sarah Parker","Manager","HR","60000")
```

**Output:**

![Output8](output.png)![Screenshot 2025-04-28 143107](https://github.com/user-attachments/assets/90609afc-a3fd-4c8e-a198-8c3de4c29f10)


**Question 9**
---
-- Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
For example:

Test	Result
pragma table_info('Reviews');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           ReviewID    INTEGER     0                       0
1           ProductID   INTEGER     0                       0
2           Rating      REAL        0                       0
3           ReviewText  TEXT        0                       0

```sql
-- create table Reviews(
ReviewID INTEGER ,
ProductID INTEGER ,
Rating REAL,
ReviewText TEXT );
```

**Output:**

![Output9](output.png)![Screenshot 2025-04-28 142822](https://github.com/user-attachments/assets/fb6ad2a3-7420-41c6-b4af-a39d3063bd8b)


**Question 10**
--- Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
For example:

Test	Result
select * from student_details;
RollNo      Name           Gender      Subject     MARKS
----------  -------------  ----------  ----------  ----------
1           Alice Johnson  Female      Math        85
2           Bob Smith      Male        Science     90
3           Charlie Brown  Male        English     78
--

```sql
-- insert into student_details(RollNo,Name,Gender,Subject,MARKS)
select  RollNo,Name,Gender,Subject,MARKS from Archived_students ;
```

**Output:**

![Output10](output.png)![Screenshot 2025-04-28 142912](https://github.com/user-attachments/assets/0814e3c8-bb7e-4a6c-86e7-7fa9f476088a)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
