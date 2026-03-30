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
```
Write a SQL statement to change salary of employee to 8000 whose Employee ID is 105, if the existing salary is less than 5000.
Employees table--------------
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
Test Result
SELECT EMPLOYEE_ID, FIRST_NAME, SALARY, PHONE_NUMBER FROM EMPLOYEES 
WHERE EMPLOYEE_ID=105;
EMPLOYEE_ID  FIRST_NAME  SALARY      
PHONE_NUMBER-----------  ----------  ----------  ------------
105          David       8000        
590.423.4569
```
```
update Employees set salary=8000
where employee_id=105 and salary<5000;
```
**Output:**

<img width="614" height="204" alt="image" src="https://github.com/user-attachments/assets/a14a973d-d437-4b3c-9602-786e9419ef2d" />


**Question 2**
```
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'
Sample table: Doctors
attributes: doctor_id, first_name, last_name, specialization
```
```
delete from doctors
where specialization='Cardiology';
```

**Output:**

<img width="612" height="365" alt="image" src="https://github.com/user-attachments/assets/48749b1c-7c87-47ad-8370-53cefe8caea5" />


**Question 3**
```
Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in
the products table.
Products Table 
name          type       ----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               
For example:
Test Result--pragma table_info('products');
select changes();
changes()---------
2
```
```
update products set reorder_lvl=reorder_lvl*0.7
where cost_price>50 and quantity<100;
```

**Output:**

<img width="617" height="103" alt="image" src="https://github.com/user-attachments/assets/bdbe4d02-b683-4735-98ea-d9dd96069aaf" />


**Question 4**
```
Write a query to fetch 5 to 9 records from EmployeeInfo table.
EmpID EmpFname EmpLname Department Project Address DOB Gender
1 Sanjay Mehra HR P1 Hyderabad(HYD)01/12/1976M
2 Ananya Mishra Admin P2 Delhi(DEL) 02/05/1968 F
 
 
For example:
Result
EmpID       EmpFname    EmpLname    Department  Project     Address     DOB         Gender----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------
5           Ankit       Kapoor      Admin       P2          Delhi(DEL)  1994-07-03    M
```
```
select *from EmployeeInfo
where EmpID between 5 and 9;
```
**Output:**

<img width="610" height="202" alt="image" src="https://github.com/user-attachments/assets/c61dfc01-d840-4de4-a065-f49b840a83a2" />


**Question 5**
```
Write a SQL query to determine the status of decimal in the Calculations table as 'Below Average', 'Average', or 'Above Average'
based on whether it is below 50, exactly 50, or above 50.
cid         name        type        notnull     dflt_value  pk----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 
For example:
Result
id          decimal     status----------  ----------  ------------
1           123.4567    Above Average
2           567.891     Above Average
3           78.234      Above Average
4           45.78       Below Average
```
```
select 
    id,decimal,
    CASE
       when decimal<50 then  'Below Average'
       when decimal=50 then 'Average'
       else 'Above Average'
    end as status
from Calculations;
```
**Output:**

<img width="614" height="311" alt="image" src="https://github.com/user-attachments/assets/a9bf60a5-8dd2-41b2-9fbb-94b45274718a" />


**Question 6**
```
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is greater than or equal to 2.
 
Sample table: Customer
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | 
PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     
7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     
2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     
6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:
Test Result
select distinct(grade)from customer; GRADE----------
2
3
1
0
GRADE----------
1
0
```
```
delete from customer
where GRADE>=2;
```
**Output:**

<img width="610" height="315" alt="image" src="https://github.com/user-attachments/assets/a3db8ec9-6c09-42fe-92fb-b60b04df17db" />


**Question 7**
```
Write a SQL statement to Find all those customers with all information whose names are ending with the letter 'n'.
customer table
cid           name             type      notnu  dflt_value    pk------------  ---------------  --------  -----  ------------  ----------
0             customer_id      int       0                    0
1             cust_name        text      0                    0
2             city             text      0                    0
3             grade            int       0                    0
4             salesman_id      int       0                    0
```
```
select *from customer
where cust_name LIKE '%n';
```

**Output:**

<img width="611" height="371" alt="image" src="https://github.com/user-attachments/assets/a44066dd-7a09-420c-87e9-d904ff4ac523" />


**Question 8**
```
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table
name               type
--------------  ----------
product_id         INT
product_name       VARCHAR(10)
category           VARCHAR(50)
cost_price         DECIMAL(10)
sell_price         DECIMAL(10)
reorder_lvl        INT
quantity              INT
supplier_id           INT
For example:

Test	Result
select changes();
changes()
----------
4

```
```
update products
set reorder_lvl=reorder_lvl*1.30
where category='Food' and quantity<reorder_lvl*0.5;
```

**Output:**

<img width="1323" height="303" alt="image" src="https://github.com/user-attachments/assets/ef387cb9-8621-4c66-a491-72e373d6acc2" />


**Question 9**
```
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes: doctor_id, first_name, last_name, specialization
```
```
delete from doctors
where specialization =  'Pediatrics' and first_name='Michael';
```

**Output:**

<img width="1321" height="265" alt="image" src="https://github.com/user-attachments/assets/e17fbe7b-3157-41be-a0c5-5f0fe81e2580" />


**Question 10**
```
Write a SQL query to identify products where the discount amount is greater than $50. Return product_id, original_price, discount_percentage, and discount_amount.

Sample table: products

product_id | original_price | discount_percentage 

------------+----------------+--------------------- 

101 | 100.00 | 0.60 

102 | 150.00 | 0.40 

103 | 200.00 | 0.10

 

For example:

Result
product_id  original_price  discount_percentage  discount_amount
----------  --------------  -------------------  ---------------
101         100             0.6                  60.0
102         150             0.4                  60.0
```
```
select product_id, original_price, discount_percentage,
original_price * discount_percentage As discount_amount
from products
where original_price * discount_percentage >50.0;
```
**Output:**

<img width="1322" height="197" alt="image" src="https://github.com/user-attachments/assets/0e97ed43-970f-47ab-90e5-2296bf564c66" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
