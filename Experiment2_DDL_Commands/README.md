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
```
Create a table named Tasks with the following columns:

TaskID as INTEGER
TaskName as TEXT
DueDate as DATE
For example:

Test	Result
pragma table_info('Tasks');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           TaskID      INTEGER     0                       0
1           TaskName    TEXT        0                       0
2           DueDate     DATE        0                       0
```
```
CREATE TABLE tasks(
   TaskID  INTEGER,
   TaskName  TEXT,
   DueDate DATE
);
```
**Output:**

<img width="1321" height="268" alt="image" src="https://github.com/user-attachments/assets/5d449f8a-6066-466c-84a4-7b291e521ed2" />


**Question 2**
```
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	Result
select * from Books;
ISBN            Title           Author              Publisher      YearPublished
--------------  --------------  ------------------  -------------  -------------
978-1234567890  The Lost World  Arthur Conan Doyle  Vintage Books  1912
978-0987654321  Gone with the   Margaret Mitchell   Macmillan      1936
978-1122334455  Moby Dick       Herman Melville     Harper & Brot  1851
```
```
INSERT INTO Books
SELECT * FROM Out_of_print_books;
```
**Output:**
<img width="1327" height="214" alt="image" src="https://github.com/user-attachments/assets/ab4cea4b-900a-4262-b75c-d647ab7da212" />

**Question 3**
```
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           discount     DECIMAL(5,2)                       0                       0
```
```
ALTER TABLE customer
ADD discount DECIMAL(5,2);
```
**Output:**
<img width="1323" height="273" alt="image" src="https://github.com/user-attachments/assets/3eef9865-26d3-45a8-8caf-83dc078e3244" />


**Question 4**
```
Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE
For example:

Test	Result
pragma table_info('Employees');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     EmployeeID  INTEGER     0                       0
1     FirstName   TEXT        0                       0
2     LastName    TEXT        0                       0
3     HireDate    DATE        0                       0
```
```
CREATE TABLE employees(
    EmployeeID INTEGER,
    FirstName TEXT,
    LastName TEXT,
    HireDate DATE
);
```

**Output:**
<img width="1322" height="221" alt="image" src="https://github.com/user-attachments/assets/6125d3e6-1a94-4ca2-9165-d27b16ac73d8" />


**Question 5**
```
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-01   100.0       2024-09-01  1
```
```
CREATE TABLE Invoices(
     InvoiceID INTEGER PRIMARY KEY,
     InvoiceDate DATE,
     Amount Real check(Amount > 0),
     DueDate DATE check(DueDate > InvoiceDate),
     OrderID INTEGER,
     foreign key(OrderId) references Orders(OrderID)
);
```

**Output:**
<img width="1323" height="228" alt="image" src="https://github.com/user-attachments/assets/e76a76bd-6e59-439b-92b8-af9f6beddc9d" />


**Question 6**
```
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT
For example:

Test	Result
pragma table_info('Locations');
cid       name             type        notnull     dflt_value  pk
--------  ---------------  ----------  ----------  ----------  ----------
0         LocationID       INTEGER     0                       0
1         LocationName     TEXT        0                       0
2         Address          TEXT        0                       0
```
```
create table Locations(
    LocationID INTEGER,
    LocationName TEXT,
    Address TEXT
);
```
**Output:**
<img width="1326" height="284" alt="image" src="https://github.com/user-attachments/assets/b90d25f0-083f-47a0-a336-3cd040700487" />


**Question 7**
```
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.
 
For example:

Test	Result
SELECT RollNo, Name, Gender 
FROM Student_details 
WHERE RollNo = 204;


RollNo      Name          Gender
----------  ------------  ----------
204         Samuel Black  M
```
```
INSERT INTO Student_details(RollNo,Name,Gender)
Values(204,'Samuel Black','M');
```
**Output:**
<img width="1329" height="231" alt="image" src="https://github.com/user-attachments/assets/348e06c5-fae7-4cd0-8b9a-95107bc8aeba" />


**Question 8**
```
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      MobileNumber     NUMBER           0                  0
6      Address          VARCHAR(100)     0                  0
```
```
ALTER TABLE Student_details
ADD MobileNumber NUMBER;
ALTER TABLE Student_details
ADD Address VARCHAR(100);
```

**Output:**

<img width="1327" height="273" alt="image" src="https://github.com/user-attachments/assets/fd0e8f40-c7ef-40cc-8a58-e9a364ac99ff" />


**Question 9**
```
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

For example:

Test	Result
SELECT ProductID, Name, Category, Price, Stock 
FROM Products 
WHERE ProductID = 104;
ProductID   Name        Category     Price       Stock
----------  ----------  -----------  ----------  ----------
104         Tablet      Electronics  100         50
```
```
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
Values('104','Tablet','Electronics','100','50');
```
**Output:**
<img width="1323" height="171" alt="image" src="https://github.com/user-attachments/assets/835dfc4f-45c7-4514-8a48-941b0cef6da2" />


**Question 10**
```
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE
For example:

Test	Result
pragma table_info('Events');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           EventID     INTEGER     0                       0
1           EventName   TEXT        0                       0
2           EventDate   DATE        0                       0
```
```
CREATE TABLE Events(
    EventID  INTEGER,
    EventName  TEXT,
    EventDate  DATE
);
```

**Output:**

<img width="1329" height="269" alt="image" src="https://github.com/user-attachments/assets/4cc63dc7-239f-41d2-9294-d1148eae8a1f" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
