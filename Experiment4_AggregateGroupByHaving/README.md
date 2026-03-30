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
```
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MINIMUM
----------
65.26
```
```
select MIN(purch_amt) as MINIMUM
from orders;
```

**Output:**

<img width="1328" height="237" alt="image" src="https://github.com/user-attachments/assets/7e4687c0-cf33-4735-8018-e1a353c6306f" />


**Question 2**
```
Write a SQL query to calculate the total number of working hours of all employees

Sample table: employee1
For example:

Result
Total working hours
-------------------
111
```
```
select SUM(workhour) as "Total working hours"
from employee1;
```

**Output:**

<img width="1319" height="237" alt="image" src="https://github.com/user-attachments/assets/07c48da1-2d86-4f6b-8b2d-537e1c4e852f" />


**Question 3**
```
Write a SQL query to find the difference between the maximum and minimum price of fruits?

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
price_diff
----------
4.65
```
```
select MAX(price)-MIN(price) as price_diff
from fruits;
```

**Output:**

<img width="1328" height="258" alt="image" src="https://github.com/user-attachments/assets/c2ccc76a-78e2-47af-aaa2-2df72f9f7f78" />


**Question 4**
```
What is the average dosage prescribed for each medication?

Sample tablePrescriptions Table
For example:

Result
Medication     AvgDosage
-------------  ----------
Ciprofloxacin  500.0
Doxorubicin    60.0
Ibuprofen      400.0
Levothyroxine  50.0
Lisinopril     10.0
MMR            0.5
Pending        0.0
Prenatal vita  1.0
Sertraline     50.0
Topiramate     25.0
```
```
select Medication,AVG(Dosage) as "AvgDosage"
from Prescriptions
group by Medication;
```

**Output:**
<img width="1330" height="536" alt="image" src="https://github.com/user-attachments/assets/5fb253e1-dc11-436c-a9d7-99c6a7c9207f" />

**Question 5**
```
How many male and female doctors are there in each medical specialty?

Sample table:Doctors Table

For example:

Result
Specialty          Gender    TotalDoctors
-----------------  --------  --------------
Cardiology         Male      1
Dermatology        Male      1
Gastroenterology   Female    4
Gastroenterology   Male      1
Pediatrics         Female    1
Pediatrics         Male      2
```
```
select Specialty,Gender,COUNT(DoctorID) as TotalDoctors
from Doctors
group by Specialty,Gender;
```

**Output:**
<img width="1319" height="482" alt="image" src="https://github.com/user-attachments/assets/3439edbf-1cc1-42ed-b7e6-01b1bf1df500" />


**Question 6**
```
How many patients are there in each city?

Sample table: Patients Table

For example:

Result
Address     TotalPatients
----------  -------------
Berlin      3
Chicago     4
Mexico      3
```
```
select Address,COUNT(PatientID) as TotalPatients
from Patients
group by Address;
```


**Output:**

<img width="1324" height="321" alt="image" src="https://github.com/user-attachments/assets/dc894cb9-a8b8-4f9c-8f24-6b7ce5c567cb" />

**Question 7**
```
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.

Sample table: employee1

For example:

Result
jdate       SUM(workhour)
----------  -------------
2004.0      46
2006.0      46
```
```
select jdate,SUM(workhour) as "SUM(workhour)"
from employee1
group by jdate
having SUM(workhour)>40;
```
**Output:**

<img width="1327" height="303" alt="image" src="https://github.com/user-attachments/assets/1f446979-b1c6-410d-8e80-d920adcf0aba" />


**Question 8**
```
Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.

Sample table: customer1

For example:

Result
age_group   MIN(age)
----------  ----------
20          22

```
```
select (age/5)*5 as "age_group", MIN(age) as "MIN(age)"
from customer1
group by (age/5)*5
having MIN(age)<25;
```

**Output:**
<img width="1326" height="265" alt="image" src="https://github.com/user-attachments/assets/52ee5dc6-9557-4ea6-ae02-b0edc3a23cc1" />


**Question 9**
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
select category_id, count(product_name) as "count(product_name)"
from products
group by category_id
having category_id<3;
```
**Output:**

<img width="1327" height="292" alt="image" src="https://github.com/user-attachments/assets/62e14c3e-6eec-4099-8071-bcc0e71e250c" />


**Question 10**
```
Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.

Sample table: employee1



For example:

Result
occupation  SUM(workhour)
----------  -------------
Business    30
Doctor      30
Engineer    24
Teacher     27
```
```
select occupation,SUM(workhour) as 'SUM(workhour)'
from employee1
group by occupation
having SUM(workhour)>20;
```
**Output:**

<img width="1323" height="346" alt="image" src="https://github.com/user-attachments/assets/cf678376-6b59-4859-ace1-4fd049451c61" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
