# Content <a class="anchor" id="content"></a>

1. [Basic SQL](#01)
2. [SQL JOIN](#02)
    * [02.01 Inner Join/Join](#02.01)
    * [02.02 Left Join/Left Outer Join](#02.02)
    * [02.03 Right Join/Right Outer Join](#02.03)
    * [02.04 Full join](#02.04)

# 01. BASIC SQL <a class="anchor" id="01"></a>

# 02. SQL JOIN <a class="anchor" id="02"></a>

A JOIN clause is used to combine rows from two or more tables, based on
a related column between them. **

The join keyword merges two or more tables and creates a temporary image
of the merged table. Then according to the conditions provided, it
extracts the required data from the image table, and once data is
fetched, the temporary image of the merged tables is dumped.

 

**Create the sample employee database to understand the join(we are
going to create under emp schema)**

```sql
CREATE SCHEMA IF NOT EXISTS schema_name AUTHORIZATION user_name;

--i.e:

`CREATE SCHEMA IF NOT EXISTS emp AUTHORIZATION postgres;`
```

**Help**
```
[user_name]=postgres
[schema_name]=emp
```
<br></br>
**creating employee table under emp schema**
```sql
drop table if exists emp.employee;

create table if not exists emp.employee
(
emp_id varchar(20),
emp_name varchar(50),
salary int,
dept_id varchar(20),
manager_id varchar(20)
);

-- sample records
insert into emp.employee values
('E1, 'Rahul', 15000, 'D1', 'M1'),
('E2', 'Manoj', 15000, 'D1', 'M1'),
('E3', 'James', 55000, 'D2', 'M2'),
('E4', 'Michael', 25000, 'D2', 'M2'),
('E5', 'Ali', 20000, 'D10', 'M3'),
('E6', 'Robin', 35000, 'D10', 'M3');
```

<br></br>
**Creating department table under emp schema**
```sql
drop table if exists emp.department;

create table if not exists emp.department
(
dept_id varchar(20),
dept_name varchar(50)
); 

-- Sample records
insert into emp.department values
('D1', 'IT'),
('D2', 'HR'),
('D3', 'Finance'),
('D4', 'Admin');
```
 
<br></br>
**Creating manager table under emp schema**
```sql
drop table if exists emp.manager;

create table if not exists emp.manager
(
manager_id varchar(20),
manager_name varchar(50),
dept_id varchar(20)
); 

-- Sample records

insert into emp.manager values
('M1', 'Prem', 'D3'),
('M2', 'Shripadh', 'D4'),
('M3', 'Nick', 'D1'),
('M4', 'Cory', 'D1');
```

<br></br>
**Creating product table under emp schema**
```sql
drop table if exists emp.projects;

create table if not exists emp.projects
(
project_id varchar(20),
project_name varchar(100),
team_member_id varchar(20)
);

-- Sample records

insert into emp.projects values
('P1', 'Data Migration', 'E1'),
('P1', 'Data Migration', 'E2'),
('P1', 'Data Migration', 'M3'),
('P2', 'ETL Tool', 'E1'),
('P2', 'ETL Tool', 'M4');
```
 
<br></br>
 **Below are the all table under emp schema**
```sql
SELECT * FROM emp.employee;
SELECT * FROM emp.department;
SELECT * FROM emp.manager;
SELECT * FROM emp.projects;
```
[↵ Back to Contenet](#content)

<br></br>
**Q1. FETCH THE EMPLOYEE NAME AND THE DEPARTMENT NAME THEY BELONG TO:**  
In order to fetch the employee name and department name we need to join the tables{employee and department} to fetch these detail.


## 02.01 INNER JOIN / JOIN<a class="anchor" id="02.01"></a>
- **Only return the matching value from both the table.** **
- It can represented by keyword "join" or "inner join" in any case.
- **ON Condition:** Column which present in both table. Column name can be different but the value should be present in the table.
- with using inner join lets try to solve the above problem:

```sql
SELECT
emp_table.emp_name,
dep_table.dept_name
FROM emp.employee emp_table
INNER JOIN emp.department dep_table
ON emp_table.dept_id=dep_table.dept_id;
```
[↵ Back to Contenet](#content)



<br></br>
**Q2 FETCH THE ALL EMPLOYEE NAME AND THE DEPARTMENT NAME THEY BELONG TO:**    
In-order to fetch the employee name and department name we need
to join the tables{employee and department} to fetch these
detail.

## 02.02 LEFT JOIN / LEFT OUTER JOIN<a class="anchor" id="02.02"></a>

- **LEFT JOIN = INNER JOIN + any additional records in the left table.** **
- In case of if any record present in left table but not present in right then we will get the Null as result.
- In case of join condition fail, it will return the "null" for right table but from left table all the records will return.
- With using inner join lets try to solve the above problem.

```sql
SELECT
emp_table.emp_name,
dep_table.dept_name
FROM emp.employee emp_table
LEFT JOIN emp.department dep_table
ON emp_table.dept_id=dep_table.dept_id;
```
[↵ Back to Contenet](#content)
<br></br>



## 02.03 RIGHT JOIN / RIGHT OUTER JOIN<a class="anchor" id="02.03"></a>

- **RIGHT JOIN = INNER JOIN + any additional records in the right table.** **
- In case of if any record present in right table but not present in left then we will get the Null as result.
- In case of join condition fail, it will rerun the "null" for lef ttable but from right table all the records will return.
- With using inner join lets try to solve the above problem.

 
```sql
SELECT
emp_table.emp_name,
dep_table.dept_name
FROM emp.employee emp_table
RIGHT JOIN emp.department dep_table
ON emp_table.dept_id=dep_table.dept_id;
```
<br></br>



**Select all the tables:**
```sql
SELECT * FROM emp.employee;
SELECT * FROM emp.department;
SELECT * FROM emp.manager;
SELECT * FROM emp.projects;
```
 <br></br>



**Fetch details of all emp, their manager, their department and the projects they work on.**
```sql
SELECT e.emp_name, m.manager_name, d.dept_name, p.project_name
FROM emp.employee e
JOIN emp.manager m ON m.manager_id = e.manager_id
LEFT JOIN emp.department d ON d.dept_id = e.dept_id
LEFT JOIN emp.projects p ON p.team_member_id=e.emp_id;
```
[↵ Back to Contenet](#content)
<br></br>


**Creating some sample schema to understand the other joins**
```sql
drop table if exists employee;
create table if not exists employee
(
	emp_id			varchar(20),
	emp_name		varchar(50),
	salary			int,
	dept_id			varchar(20),
	manager_id		varchar(20)
);
insert into employee values
('E1', 'Rahul', 15000, 'D1', 'M1'),
('E2', 'Manoj', 15000, 'D1', 'M1'),
('E3', 'James', 55000, 'D2', 'M2'),
('E4', 'Michael', 25000, 'D2', 'M2'),
('E5', 'Ali', 20000, 'D10', 'M3'),
('E6', 'Robin', 35000, 'D10', 'M3');


drop table if exists department;
create table if not exists department
(
	dept_id			varchar(20),
	dept_name		varchar(50)
);
insert into department values
('D1', 'IT'),
('D2', 'HR'),
('D3', 'Finance'),
('D4', 'Admin');

drop table if exists company;
create table if not exists company
(
	company_id		varchar(10),
	company_name	varchar(50),
	location		varchar(20)
);
insert into company values
('C001', 'techTFQ Solutions', 'Kuala Lumpur');

insert into company values
('C002', 'techTFQ Media Group', 'Singapore');


DROP TABLE if exists family;
CREATE TABLE if not exists family
(
    member_id     VARCHAR(10),
    name          VARCHAR(50),
    age           INT,
    parent_id     VARCHAR(10)
);
insert into family values
  ('F1', 'David', 4, 'F5'),
  ('F2', 'Carol', 10, 'F5'),
  ('F3', 'Michael', 12, 'F5'),
  ('F4', 'Johnson', 36, ''),
  ('F5', 'Maryam', 40, 'F6'),
  ('F6', 'Stewart', 70, ''),
  ('F7', 'Rohan', 6, 'F4'),
  ('F8', 'Asha', 8, 'F4');
```

Run above sql query to create table to undertand rest joins.    
[↵ Back to Contenet](#content)
<br></br>


## 02.04 Full Join<a class="anchor" id="02.04"></a>
- **INNER JOIN + all remaining records from left + all remaining records from right table.** **
- Return all the records from both table.
- substituting NULL for any row value that is not present in the other table.

```
FULL Join = INNER Join + all remaining records from Left Table (returns null value for any columns fetched from right table) 
                       + all remaining records from Right Table (returns null value for any columns fetched from left otable)
```

