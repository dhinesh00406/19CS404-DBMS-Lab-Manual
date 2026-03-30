# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
```
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:
<img width="581" height="99" alt="image" src="https://github.com/user-attachments/assets/627c7a18-f741-4d3e-a63e-d6e6be338035" />

APPOINTMENTS TABLE:
<img width="585" height="91" alt="image" src="https://github.com/user-attachments/assets/35e417d8-2213-48df-bff0-8ac9082d3b4c" />

For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
1                Alice            Williams         1980-05-12       2024-01-10                      1
```
```
select p.*
from patients as p
inner join appointments as a
on a.patient_id=p.patient_id
where a.appointment_date BETWEEN '2024-01-01' and '2024-01-31';
```

**Output:**

<img width="1300" height="372" alt="image" src="https://github.com/user-attachments/assets/9b99a01d-d434-4c74-bf74-bd3e8e02f0e1" />

**Question 2**
```
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with a date of birth after '1990-01-01'.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE

For example:

Result
first_name       surgery_id       patient_id       surgeon_id       surgery_date
---------------  ---------------  ---------------  ---------------  ------------
Bob              2                2                2                2024-02-28
```
```
select p.first_name,s.*
from patients as p
inner join surgeries as s
on s.patient_id=p.patient_id
where p.date_of_birth >  '1990-01-01';
```

**Output:**

<img width="1297" height="352" alt="image" src="https://github.com/user-attachments/assets/5a3018ec-53d5-43bd-8268-6a906c7554af" />


**Question 3**
```
Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE

For example:

Result
first_name       last_name
---------------  ---------------
Alice            Williams
```
```
select p.first_name,p.last_name
from patients as p
inner join surgeries as s
on s.patient_id=p.patient_id
where s.surgery_date between '2024-01-01' and '2024-01-31';
```

**Output:**

<img width="1312" height="353" alt="image" src="https://github.com/user-attachments/assets/3b39bedb-43ad-4aa9-a2d4-80c60affe75c" />

**Question 4**
```
Write the SQL query that accomplishes the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a non-null discharge date.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)

For example:

Result
patient_name     doctor_name
---------------  ---------------
Bob              Emily
```
```
select p.first_name as 'patient_name',d.first_name as 'doctor_name'
from patients as p
inner join doctors as d
on d.doctor_id=p.doctor_id
where p.discharge_date is NOT NULL;
```
**Output:**

<img width="1299" height="354" alt="image" src="https://github.com/user-attachments/assets/9b231bf0-bca6-4b05-8221-cc540abc728c" />

**Question 5**
```
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:
<img width="572" height="96" alt="image" src="https://github.com/user-attachments/assets/482986c3-14ee-4ddb-9b11-b0752fa36b73" />

APPOINTMENTS TABLE:
<img width="587" height="93" alt="image" src="https://github.com/user-attachments/assets/4ed19cbd-745b-42a4-9099-44c90c71ef9d" />

For example:

Result
date_of_birth    appointment_id   patient_id       doctor_id        appointment_date
---------------  ---------------  ---------------  ---------------  -------------------
1980-05-12       1                1                1                2024-01-05 10:00:00
```
```
select p.date_of_birth,a.*
from patients as p
inner join appointments as a
on a.patient_id=p.patient_id
where p.first_name='Alice';
```
**Output:**

<img width="1297" height="374" alt="image" src="https://github.com/user-attachments/assets/0640ac30-ac4b-4533-9ad0-ada9dc3ff398" />


**Question 6**
```
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test names 'Blood Test' or 'Blood Pressure' and results not containing the substring 'Normal'.

PATIENTS TABLE:
<img width="582" height="91" alt="image" src="https://github.com/user-attachments/assets/7d63a32f-2f73-4c64-a5c2-72af10f54dc4" />

TEST_RESULT TABLES:
<img width="579" height="87" alt="image" src="https://github.com/user-attachments/assets/ec2475c7-4e1f-416b-9ff2-78cc70f00418" />

For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
1                Alice            Williams         1980-05-12       2024-01-10                      1
```
```
select p.*
from patients as p
inner join test_results as t
on t.patient_id=p.patient_id
where t.test_name IN ('Blood Test' , 'Blood Pressure') 
and t.result NOT LIKE '%Normal%';
```
**Output:**

<img width="1299" height="376" alt="image" src="https://github.com/user-attachments/assets/d6f2823f-85c7-4a6b-8c51-07116deef8a4" />

**Question 7**
```
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

PATIENTS TABLE:
<img width="582" height="94" alt="image" src="https://github.com/user-attachments/assets/4ddb3614-403e-48c1-9856-263d3419744b" />

TEST_RESULT TABLES:
<img width="582" height="92" alt="image" src="https://github.com/user-attachments/assets/13f579c1-690a-499f-adbd-0f07636baa4c" />

For example:

Result
patient_name     result_id        patient_id       test_name        result      test_date
---------------  ---------------  ---------------  ---------------  ----------  ----------
Alice            1                1                Blood Pressure   120/80      2024-01-20
```
```
select p.first_name as 'patient_name',t.*
from patients as p
inner join test_results as t
on t.patient_id=p.patient_id
where t.test_name='Blood Pressure';
```
**Output:**

<img width="1305" height="373" alt="image" src="https://github.com/user-attachments/assets/4d96fb90-663a-4d13-8005-854cb90ee9b8" />

**Question 8**
```
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

PATIENTS TABLE:
<img width="582" height="92" alt="image" src="https://github.com/user-attachments/assets/f789c583-9df6-4064-9758-76453afd867e" />

TEST_RESULT TABLES:
<img width="580" height="91" alt="image" src="https://github.com/user-attachments/assets/c6f8a8f4-03d5-4794-b2cf-262d651b94c0" />

For example:

Result
patient_name
---------------
Alice
```
```
select p.first_name as 'patient_name'
from patients as p
inner join test_results as t
on t.patient_id = p.patient_id
where t.test_name='Blood Pressure';
```


**Output:**
<img width="1296" height="350" alt="image" src="https://github.com/user-attachments/assets/5d1ab61f-2a79-456c-8647-3d23bf846c49" />


**Question 9**
```
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
cust_name        city             ord_no           ord_date         Order Amount  name        commission
---------------  ---------------  ---------------  ---------------  ------------  ----------  ----------
Nick Rimando     Chennai          70002            2012-10-05       65.26         Bob Emily   0.15
Nick Rimando     Chennai          70008            2012-09-10       5760.0        Bob Emily   0.15
Nick Rimando     Chennai          70013            2012-04-25       3045.6        Bob Emily   0.15
Graham Zusi      California       70001            2012-10-05       150.5         Nail Knite  0.13
Graham Zusi      California       70007            2012-09-10       948.5         Nail Knite  0.13
Brad Guzan       London           70009            2012-09-10       270.65        Pit Alex    0.11
Fabian Johns     Paris            70010            2012-10-10       1983.43       Mc Lyon     0.14
Brad Davis       New York         70005            2012-07-27       2400.6        Bob Emily   0.15
Geoff Cameron    Berlin           70003            2012-10-10       2480.4        Lauson Hen  0.12
Geoff Cameron    Berlin           70004            2012-08-17       110.5         Lauson Hen  0.12
Julian Green     London           70012            2012-06-27       250.45        Nail Knite  0.13
Jozy Altidore    Moscow           70011            2012-08-17       75.29         Paul Adam   0.13
```
```
select c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt as 'Order Amount',s.name,s.commission
from customer c
left join orders as o
on c.customer_id=o.customer_id
left join salesman as s
on c.salesman_id=s.salesman_id;
```

**Output:**

<img width="1298" height="975" alt="image" src="https://github.com/user-attachments/assets/eef16ae8-5d97-4acb-bff0-f613da9bc58a" />


**Question 10**
```
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n"), with an inner join on the "department_id" column and a condition filtering for nurses in the 'Pediatrics' department.

NURSES TABLE:
<img width="583" height="97" alt="image" src="https://github.com/user-attachments/assets/d56eebf3-c85c-4c9d-b133-a4a1788193ea" />

DEPARTMENTS TABLE:
<img width="581" height="98" alt="image" src="https://github.com/user-attachments/assets/85e692e4-0cc4-4fd7-ae02-f93a88b3668e" />

For example:

Result
nurse_id         first_name       last_name        department_id
---------------  ---------------  ---------------  ---------------
3                Sophia           Clark            3
```
```
select n.*
from nurses as n
inner join departments as d
on d.department_id=n.department_id
where department_name='Pediatrics';
```

**Output:**

<img width="1298" height="346" alt="image" src="https://github.com/user-attachments/assets/4600b80e-ff2d-46f3-89e6-ba36d03fc8f8" />

## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
