# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```
**Question 1**
--
--
```
How many doctors specialize in each medical specialty?

Sample table:Doctors Table



For example:

Result
Specialty          TotalDocto
-----------------  ----------
Gastroenterology   1
Neurology          1
Obstetrics         3
Ophthalmology      1
Orthopedics        1
Pediatrics         2
Urology            1


```
```
sql
-- SELECT Specialty, COUNT(*) AS TotalDoctor
FROM Doctors
GROUP BY Specialty;
```

**Output:**

![Output1](output.png)![Screenshot 2025-04-30 112646](https://github.com/user-attachments/assets/8bf4ce21-4041-4d37-9a7a-6239b0ba4a41)


**Question 2**
---
--
```
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT
For example:

Result
PatientID   TotalAppointments
----------  -----------------
3           3
5           2
6           1
7           1
10          3

```
```
sql
-- SELECT PatientID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;
```

**Output:**

![Output2](output.png)![Screenshot 2025-04-30 112714](https://github.com/user-attachments/assets/6fda6025-edf9-4f7d-a826-c31c3d197141)


**Question 3**
---
--
```
What is the total number of medications prescribed for each patient?

Sample tablePrescriptions Table



For example:

Result
PatientID   TotalMedications
----------  ----------------
1           1
2           1
3           1
4           1
5           1
6           1
7           1
8           1
9           1
10          1


```
```
sql
--SELECT PatientID, COUNT(*) AS TotalMedications
FROM Prescriptions
GROUP BY PatientID;
```

**Output:**

![Output3](output.png)![Screenshot 2025-04-30 112714](https://github.com/user-attachments/assets/ea8ff435-8eb9-4aad-b7f3-e735ebfb4e6e)


**Question 4**
---
--
```
Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.

Sample table: customer



 

For example:

Result
COUNT
----------
9

```
```
sql
-- SELECT COUNT(*) AS COUNT
FROM customer
WHERE city <> 'Noida';
```

**Output:**

![Output4](output.png)![Screenshot 2025-04-30 112745](https://github.com/user-attachments/assets/b8d2eed0-1c49-478a-a36f-1f12902faf50)


**Question 5**
---
-- 
```
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
total
----------
225

```
```
sql
-- SELECT SUM(inventory) AS total
FROM fruits
WHERE unit = 'LB';
```

**Output:**

![Output5](output.png)![Screenshot 2025-04-30 112804](https://github.com/user-attachments/assets/74eca106-6520-49cd-99cf-4fc9409e4abb)


**Question 6**
---
--
```
Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
age_difference
--------------
13

```
```
sql
--SELECT MAX(age) - MIN(age) AS age_difference
FROM employee;
```

**Output:**

![Output6](output.png)![Screenshot 2025-04-30 112820](https://github.com/user-attachments/assets/85a4f455-4458-4064-984d-f17b1ab57506)


**Question 7**
---
--
```
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the total salary sum for each group, and excludes groups where the total salary sum is not greater than 5000.

Sample table: customer1



For example:

Result
age_group   SUM(salary)
----------  -----------
20          16500
25          16500

```
```
sql
-- SELECT (age / 5) * 5 AS age_group, SUM(salary) AS "SUM(salary)"
FROM customer1
GROUP BY (age / 5) * 5
HAVING SUM(salary) > 5000;
```

**Output:**

![Output7](output.png)![Screenshot 2025-04-30 112837](https://github.com/user-attachments/assets/5469aa2d-c570-4c8f-958d-c92310589c4c)


**Question 8**
---
-- 
```
Write the SQL query that accomplishes the selection of average price for each category from the "products" table and includes only those products where the average price falls between 10 and 15.

Sample table: products



For example:

Result
category_id  AVG(Price)
-----------  ----------
1            12.375

```
```
sql
-- SELECT category_id, AVG(price) AS "AVG(Price)"
FROM products
GROUP BY category_id
HAVING AVG(price) BETWEEN 10 AND 15;
```

**Output:**

![Output8](output.png)![Screenshot 2025-04-30 112851](https://github.com/user-attachments/assets/e67466ee-6681-4292-9250-35eb28902b70)


**Question 9**
---
--
```
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products



For example:

Result
category_id  count(product_name)
-----------  -------------------
1            4
2            3

```
```
sql
-- SELECT category_id, COUNT(product_name) AS "count(product_name)"
FROM products
GROUP BY category_id
HAVING MIN(category_id) < 3;
```

**Output:**

![Output9](output.png)![Screenshot 2025-04-30 112907](https://github.com/user-attachments/assets/45951802-0ea3-497a-8971-695b5e9775e7)


**Question 10**
---
-- 
```
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT
For example:

Result
PatientID   TotalAppointments
----------  -----------------
3           3
5           2
6           1
7           1
10          3


```
```
sql 
SELECT PatientID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;

```

**Output:**

![Output10](output.png)![Screenshot 2025-04-30 112714](https://github.com/user-attachments/assets/a8710281-38df-4b63-acba-5b6206a8f33e)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

