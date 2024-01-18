# CONTENT

1.  [Basic SQL](#_01._BASIC)

2.  [[SQL JOIN](#sql-join)]{.mark}

    a.  [02.01 Inner Join/ Join]{.mark}

    b.  [02.02 Left Join/ Left Outer Join]{.mark}

    c.  [02.03 Right Join / Right Outer Join]{.mark}

    d.  []{.mark}

#  01. BASIC SQL

# 02. SQL JOIN

A JOIN clause is used to combine rows from two or more tables, based on
a related column between them. \*\*

The join keyword merges two or more tables and creates a temporary image
of the merged table. Then according to the conditions provided, it
extracts the required data from the image table, and once data is
fetched, the temporary image of the merged tables is dumped.[]{.mark}

 

**Create the sample employee database to understand the join(we are
going to create under emp schema)**

CREATE SCHEMA IF NOT EXISTS schema_name AUTHORIZATION user_name;

i.e:

CREATE SCHEMA IF NOT EXISTS emp AUTHORIZATION postgres;

\--help

\[user_name\]=postgres

\[schema_name\]=emp

**creating employee table under emp schema**

drop table if exists emp.employee;

create table if not exists emp.employee

(

emp_id varchar(20),

emp_name varchar(50),

salary int,

dept_id varchar(20),

manager_id varchar(20)

);

 

\-- sample records

insert into emp.employee values

(\'E1\', \'Rahul\', 15000, \'D1\', \'M1\'),

(\'E2\', \'Manoj\', 15000, \'D1\', \'M1\'),

(\'E3\', \'James\', 55000, \'D2\', \'M2\'),

(\'E4\', \'Michael\', 25000, \'D2\', \'M2\'),

(\'E5\', \'Ali\', 20000, \'D10\', \'M3\'),

(\'E6\', \'Robin\', 35000, \'D10\', \'M3\');

[]{.mark}

**Creating department table under emp schema**

drop table if exists emp.department;

create table if not exists emp.department

(

dept_id varchar(20),

dept_name varchar(50)

); 

\-- Sample records

insert into emp.department values

(\'D1\', \'IT\'),

(\'D2\', \'HR\'),

(\'D3\', \'Finance\'),

(\'D4\', \'Admin\');

 []{.mark}

**Creating manager table under emp schema**

drop table if exists emp.manager;

create table if not exists emp.manager

(

manager_id varchar(20),

manager_name varchar(50),

dept_id varchar(20)

); 

\-- Sample records

insert into emp.manager values

(\'M1\', \'Prem\', \'D3\'),

(\'M2\', \'Shripadh\', \'D4\'),

(\'M3\', \'Nick\', \'D1\'),

(\'M4\', \'Cory\', \'D1\');

 

 

[]{.mark}

[]{.mark}

**Creating product table under emp schema[]{.mark}**

drop table if exists emp.projects;

create table if not exists emp.projects

(

project_id varchar(20),

project_name varchar(100),

team_member_id varchar(20)

);

 

\-- Sample records

insert into emp.projects values

(\'P1\', \'Data Migration\', \'E1\'),

(\'P1\', \'Data Migration\', \'E2\'),

(\'P1\', \'Data Migration\', \'M3\'),

(\'P2\', \'ETL Tool\', \'E1\'),

(\'P2\', \'ETL Tool\', \'M4\');

 

 

**Below are the all table under emp schema**

SELECT \* FROM emp.employee;

SELECT \* FROM emp.department;

SELECT \* FROM emp.manager;

SELECT \* FROM emp.projects;

[]{.mark}

[Q1. FETCH THE EMPLOYEE NAME AND THE DEPARTMENT NAME THEY BELONG
TO.]{.mark}

In order to fetch the employee name and department name we need to join
the tables{employee and department} to fetch these detail.[]{.mark}

[]{.mark}

## 02.01 INNER JOIN / JOIN

-   Only return the matching value from both the table. \*\*

-   It can represented by keyword \"join\" or \"inner join\" in any
    case.

-   ON Condition: Column which present in both table. Column name can be
    different but the value should be present in the table.

-   with using inner join lets try to solve the above problem:

 

SELECT

emp_table.emp_name,

dep_table.dept_name

FROM emp.employee emp_table

INNER JOIN emp.department dep_table

ON emp_table.dept_id=dep_table.dept_id;

[]{.mark}

[Q2 FETCH THE ALL EMPLOYEE NAME AND THE DEPARTMENT NAME THEY BELONG
TO.]{.mark}

[]{.mark}in-order to fetch the employee name and department name we need
to join the []{.mark}tables{employee and department} to fetch these
detail.[]{.mark}

[]{.mark}

## 02.02 LEFT JOIN / LEFT OUTER JOIN

-   LEFT JOIN = INNER JOIN + any additional records in the left table.
    \*\*

-   In case of if any record present in left table but not present in
    right then we will get the Null as result.

-   In case of join condition fail, it will return the \"null\" for
    right table but from left table all the records will return.

-   With using inner join lets try to solve the above problem.

 

SELECT

emp_table.emp_name,

dep_table.dept_name

FROM emp.employee emp_table

LEFT JOIN emp.department dep_table

ON emp_table.dept_id=dep_table.dept_id;

[]{.mark}

## 02.03 RIGHT JOIN / RIGHT OUTER JOIN:

-   RIGHT JOIN = INNER JOIN + any additional records in the right table.
    \*\*

-   In case of if any record present in right table but not present in
    left then we will get the Null as result.

-   In case of join condition fail, it will rerun the \"null\" for left
    table but from right table all the records will return.

-   With using inner join lets try to solve the above problem.

 

SELECT

emp_table.emp_name,

dep_table.dept_name

FROM emp.employee emp_table

RIGHT JOIN emp.department dep_table

ON emp_table.dept_id=dep_table.dept_id;

 

 

 

SELECT \* FROM emp.employee;

SELECT \* FROM emp.department;

SELECT \* FROM emp.manager;

SELECT \* FROM emp.projects;

 

\-- Fetch details of all emp, their manager, their department and the

\-- projects they work on.

SELECT e.emp_name, m.manager_name, d.dept_name, p.project_name

FROM emp.employee e

JOIN emp.manager m ON m.manager_id = e.manager_id

LEFT JOIN emp.department d ON d.dept_id = e.dept_id

LEFT JOIN emp.projects p ON p.team_member_id=e.emp_id;
