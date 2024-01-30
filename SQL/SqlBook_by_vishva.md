# Content <a class="anchor" id="content"></a>

1. [Basic SQL](#01)
2. [SQL JOIN](#02)
    * [02.01 Inner Join/Join](#02.01)
    * [02.02 Left Join/Left Outer Join](#02.02)
    * [02.03 Right Join/Right Outer Join](#02.03)
    * [02.04 Full Join/Full Outer Join](#02.04)
    * [02.05 Cross Join](#02.05)
    * [02.06 Natural Join](#02.06)
    * [02.07 SQL Join Wrapup](#02.07)

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
- It is also called **full outer join**. `outer` keyword is optional.
- Return all the records from both table.
- substituting NULL for any row value that is not present in the other table.

```sql
FULL Join = INNER Join + all remaining records from Left Table (returns null value for any columns fetched from right table) 
                       + all remaining records from Right Table (returns null value for any columns fetched from left otable)

FULL JOIN = INNER JOIN + LEFT JOIN + RIGHT JOIN                       
```

**Example**    
```sql
select e.emp_name, d.dept_name
from employee e
full join department d on d.dept_id=e.dept_id;
```

<br></br>
**Below keyword have same functionality**
```sql
left join ==> left outer join
right join ==> right out join
inner join ==> join
full join ==> full outer join
```

[↵ Back to Contenet](#content)
<br></br>

## 02.05 Cross Join <a class="anchor" id="02.05"></a>
- A cross join is a join operation that produces the `Cartesian product` of two or more tables. **
- In Math, a **Cartesian product** is a mathematical operation that returns a product set of multiple sets.
- For example, with two sets A {x,y,z} and B {1,2,3}, the Cartesian product of A x B is the set of all ordered pairs (x,1), (x,2), (x,3), (y,1) (y,2), (y,3), (z,1), (z,2), (z,3).
- Does required the join condition.


The following picture illustrates the Cartesian product of A and B:   

![alt imaage01](resource/image01)
<br></br>

**Example**
```sql
select e.emp_name, d.dept_name
from employee e --6
cross join department d ; --4
```
<br></br>


**Problem01:**    
Write a query to fetch the employee name and their corresponding department name.
also make sure to display the company name and the company location corresponding to each employee.

```sql
--CROSS JOIN
select e.emp_name, d.dept_name, c.company_name, c.location
from employee e
inner join department d on e.dept_id=d.dept_id
cross join company c;
```
[↵ Back to Contenet](#content)
<br></br>



## 02.06 Natural Join <a class="anchor" id="02.06"></a>
- A NATURAL JOIN is a JOIN operation that creates an implicit join clause for you based on the common columns in the two tables being joined. Common columns are columns that have the same name in both tables.
- A NATURAL JOIN can be an [INNER join](#02.01), a [LEFT OUTER join](#02.02), or a [RIGHT OUTER join](#02.03). The default is [INNER join](#02.01).
- Not a recommenced join since the system decide on which column name need to join the table.
- if system found the common column between table then it will perform the inner join else it will perform the full join.
<br></br>


**Create the sample table to understand the Natural Join**
```sql
create table if not exists table1(
id int
);
create table if not exists table2(
id int
);


-- insert the sample records in table1
insert into table1 values
(1),
(1),
(1),
(2),
(3),
(3),
(3);


-- insert the sample records in table2
insert into table2 values
(1),
(1),
(2),
(2),
(4),
(NULL);


--select query
select * from table1;
select * from table2;


-- NATURAL JOIN 
SELECT * FROM table1 t1
NATURAL JOIN table2 t2;
```

Since we have same column name(id) in both tables it will perform the inner join and we will get the below result:    

![alt image02](resource/image02)


Let's understand to change one of the table name to see how it does like cross join:    

```sql
-- RENAMING THE TABLE1 COLUMN ID TO ID_NEW
alter table table1 rename column id to id_new;


-- NATURAL JOIN 
SELECT * FROM table1 t1
NATURAL JOIN table2 t2;
```

Now YOU can see we are gating the 42 records since there isn't any matching columns between both the tableS.   

**SAMPLE OUTPUT**   
![alt image03](resource/image03)

[↵ Back to Contenet](#content)
<br></br>



## 02.07 WrapUP the Join<a class="anchor" id="02.07"></a>

lets create the sample table3 and table4 to understand the all join:

```sql
--Creating the table3
create table if not exists table3(
id int
);


--Creating the table4
create table if not exists table4(
id int
);


--inserting the sample value in table3
insert into table3 values
(1),
(1),
(1),
(1),
(1),
(NULL),
(NULL);


--inserting the sample value in table4
insert into table4 values
(1),
(1),
(1),
(2),
(NULL);


select * from table3;
select * from table4;
```
<br></br>


**Problem1** how many records will return in inner join:

![alt image04](resource/image04)

```sql
-- inner join
select * from table3 t3
join table4 t4
on t3.id=t4.id;
```
![alt image05](resource/image05)

<br></br>

**Problem2** How many records will return in the left join   
```sql
-- Left Join
select * from table3 t3
left join table4 t4
on t3.id=t4.id;

-- it should return the 17 records 
-- inner join + Non-matching records from left table(which are 2 nulls)
-- 15 + 2 = 17
```
![alt image06](resource/image06)


<br></br>

**Problem3** How many records will return in the right join   
```sql
-- Right Join
select * from table3 t3
right join table4 t4
on t3.id=t4.id;

-- it should return the 17 records 
-- inner join + Non-matching records from right table(which is 2 and nulls)
-- 15 + 2 = 17
```
![alt image06](resource/image06)


<br></br>

**Problem4** How many records will return in the full join   
```sql
-- Full Join
select * from table3 t3
full join table4 t4
on t3.id=t4.id;

-- it should return the 19 records 
-- inner join + Non-matching records from right table(which is 2 and nulls) + Non-matching records from left table(which are 2 nulls)

-- 15 + 2 + 2= 19
```
![alt image06](resource/image07)


<br></br>

**Problem5** How many records will return in the Natural join   
```sql
-- natural Join
select * from table3 t3
natural join table4 t4;

-- it should return the 15 records 
-- in both table3 and table4 the column(id) is matching so it will perform the inner join
-- else it will perform the cross join

-- so its should return the 15
```
![alt image06](resource/image05)


<br></br>

**Problem6** How many records will return in the cross join   
```sql
-- Full Join
select * from table3 t3
cross join table4 t4;

-- it should return the 35 records 
-- table3 = 7 and table4 = 5( 7 X 5 = 35)
-- so its should return the 35
```
![alt image06](resource/image08)
