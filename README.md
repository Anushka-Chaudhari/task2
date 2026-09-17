# task2

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| batch1343          |
| company_db         |
| emp                |
| information_schema |
| mysql              |
| performance_schema |
| student            |
| students           |
| sys                |
+--------------------+
9 rows in set (0.02 sec)

mysql> create database capgemini;
Query OK, 1 row affected (0.01 sec)

mysql> create table employee(id int PRIMARY KEY AUTO_INCREMENT,Name varchar(70) NOT NULL, Profile varchar(50) NOT NULL, Email varchar(90) UNIQUE, salary int, age int, experience int);
ERROR 1046 (3D000): No database selected
mysql> use capgemini;
Database changed
mysql> create table employee(id int PRIMARY KEY AUTO_INCREMENT,Name varchar(70) NOT NULL, Profile varchar(50) NOT NULL, Email varchar(90) UNIQUE, salary int, age int, experience int);
Query OK, 0 rows affected (0.04 sec)

mysql> insert into employee(name,profile,email,salary,age,experience)values('rani','dev','rani@gmail.com',11000,43,27),('raj','test','raj@gmail.com',21000,33,17),('radha','test','radha@gmail.com',26000,38,21),('raj','dev','raj12@gmail.com',51000,12),('john','dev','john@gmail.com',51000,39,27);
ERROR 1136 (21S01): Column count doesn't match value count at row 4
mysql> insert into employee(name,profile,email,salary,age,experience)values('rani','dev','rani@gmail.com',11000,43,27),
    -> ('raj','test','raj@gmail.com',21000,33,17),
    -> ('radha','test','radha@gmail.com',26000,38,21),
    -> ('raj','dev','raj12@gmail.com',51000,32,12),
    -> ('john','dev','john@gmail.com',51000,39,27);
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> select * from employee;
+----+-------+---------+-----------------+--------+------+------------+
| id | Name  | Profile | Email           | salary | age  | experience |
+----+-------+---------+-----------------+--------+------+------------+
|  1 | rani  | dev     | rani@gmail.com  |  11000 |   43 |         27 |
|  2 | raj   | test    | raj@gmail.com   |  21000 |   33 |         17 |
|  3 | radha | test    | radha@gmail.com |  26000 |   38 |         21 |
|  4 | raj   | dev     | raj12@gmail.com |  51000 |   32 |         12 |
|  5 | john  | dev     | john@gmail.com  |  51000 |   39 |         27 |
+----+-------+---------+-----------------+--------+------+------------+
5 rows in set (0.00 sec)

mysql> alter table employee ADD branch_location;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '' at line 1
mysql> alter table employee ADD branch_location varchar(50);
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select SUM(salary) AS Total_salary from employee;
+--------------+
| Total_salary |
+--------------+
|       160000 |
+--------------+
1 row in set (0.00 sec)

mysql> select MAX(salary) from employee where profile='test';
+-------------+
| MAX(salary) |
+-------------+
|       26000 |
+-------------+
1 row in set (0.00 sec)

mysql> select AVG(experience) from employee;
+-----------------+
| AVG(experience) |
+-----------------+
|         20.8000 |
+-----------------+
1 row in set (0.00 sec)

mysql> select name from employee where salary=(select MAX(salary) from employee);
+------+
| name |
+------+
| raj  |
| john |
+------+
2 rows in set (0.01 sec)

mysql> select name,experience from employee where salary=(select MIN(salary) from employee);
+------+------------+
| name | experience |
+------+------------+
| rani |         27 |
+------+------------+
1 row in set (0.00 sec)

mysql> select COUNT(id) AS Total_employee from employee;
+----------------+
| Total_employee |
+----------------+
|              5 |
+----------------+
1 row in set (0.00 sec)

mysql>
mysql> select * from employee WHERE profile='test' AND salary>25000;
+----+-------+---------+-----------------+--------+------+------------+-----------------+
| id | Name  | Profile | Email           | salary | age  | experience | branch_location |
+----+-------+---------+-----------------+--------+------+------------+-----------------+
|  3 | radha | test    | radha@gmail.com |  26000 |   38 |         21 | NULL            |
+----+-------+---------+-----------------+--------+------+------------+-----------------+
1 row in set (0.01 sec)

mysql> UPDATE employee SET profile='support' WHERE name='Radha';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql>
mysql> select * from employee;
+----+-------+---------+-----------------+--------+------+------------+-----------------+
| id | Name  | Profile | Email           | salary | age  | experience | branch_location |
+----+-------+---------+-----------------+--------+------+------------+-----------------+
|  1 | rani  | dev     | rani@gmail.com  |  11000 |   43 |         27 | NULL            |
|  2 | raj   | test    | raj@gmail.com   |  21000 |   33 |         17 | NULL            |
|  3 | radha | support | radha@gmail.com |  26000 |   38 |         21 | NULL            |
|  4 | raj   | dev     | raj12@gmail.com |  51000 |   32 |         12 | NULL            |
|  5 | john  | dev     | john@gmail.com  |  51000 |   39 |         27 | NULL            |
+----+-------+---------+-----------------+--------+------+------------+-----------------+
5 rows in set (0.00 sec)

mysql> select MAX(salary) from employee WHERE salary<(select MAX(salary) from employee);
+-------------+
| MAX(salary) |
+-------------+
|       26000 |
+-------------+
1 row in set (0.00 sec)

mysql> select MIN(salary) from employee WHERE salary>(select MIN(salary) from employee);
+-------------+
| MIN(salary) |
+-------------+
|       21000 |
+-------------+
1 row in set (0.00 sec)

mysql> select AVG(salary) from employee WHERE profile='dev';
+-------------+
| AVG(salary) |
+-------------+
|  37666.6667 |
+-------------+
1 row in set (0.00 sec)

mysql> select name,salary from employee WHERE experience=(select MIN(experience) from employee);
+------+--------+
| name | salary |
+------+--------+
| raj  |  51000 |
+------+--------+
1 row in set (0.00 sec)

mysql>
mysql> select name from employee where age=(select MIN(age) from employee) AND salary=(select MAX(salary) from employee);
+------+
| name |
+------+
| raj  |
+------+
1 row in set (0.00 sec)

mysql> truncate table employee;
Query OK, 0 rows affected (0.10 sec)

mysql> select * from employee;
Empty set (0.00 sec)
