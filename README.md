MANIPULATE TABLES IN A DATABASE USING SIMPLE QUERIES, NESTED QUERIES, SUB QUERIES AND JOINS 
 
COMMANDS:  
 
NESTED QUERY 
 
SQL>create table student(id number(10), name varchar2(20),classID number(10), marks varchar2(20)); 
SQL>insert into student values(1,'pinky',3,2.4); 
SQL>insert into student values(2,'bob',3,1.44); 
SQL>insert into student values(3,'Jam',1,3.24); 
SQL>insert into student values(4,'lucky',2,2.67); 
SQL>insert into student values(5,'ram',2,4.56); 
SQL>select * from student; 
  
 
SQL>Create table teacher(id number(10), name varchar(20), subject varchar2(10), classID number(10), salary number(30)); 
SQL>insert into teacher values(1,’bhanu’,’computer’,3,5000); 
SQL>insert into teacher values(2,'rekha','science',1,5000); 
SQL>insert into teacher values(3,'siri','social',NULL,4500); 
SQL>insert into teacher values(4,'kittu','mathsr',2,5500); 
SQL>select * from teacher; 
 
  
 
SQL>Create table class(id number(10), grade number(10), teacherID number(10), noofstudents number(10)); 
SQL>insert into class values(1,8,2,20); 
SQL>insert into class values(2,9,3,40); 
SQL>insert into class values(3,10,1,38); 
SQL>select * from class; 
  
SQL> Select AVG(noofstudents) from class where teacherID IN(Select id from teacher 
Where subject=’science’ OR subject=’maths’); 
20.0 
SQL> SELECT * FROM student WHERE classID = (  SELECT id   FROM class   WHERE 
2 noofstudents = (      SELECT MAX(noofstudents)      FROM class)); 
4|lucky |2|2.67 
5|ram   |2|4.56 
 
JOINS: 
EQUIJOIN. 
Table 1 − CUSTOMERS Table is as follows. 
+----+----------+-----+-----------+----------+ 
| ID | NAME     | AGE | ADDRESS   | SALARY   | 
+----+----------+-----+-----------+----------+ 
|  1 | Ramesh   |  32 | Ahmedabad |  2000.00 | 
|  2 | Khilan   |  25 | Delhi     |  1500.00 | 
|  3 | kaushik  |  23 | Kota      |  2000.00 | 
|  4 | Chaitali |  25 | Mumbai    |  6500.00 | 
|  5 | Hardik   |  27 | Bhopal    |  8500.00 | 
|  6 | Komal    |  22 | MP        |  4500.00 | 
|  7 | Muffy    |  24 | Indore    | 10000.00 | 
+----+----------+-----+-----------+----------+ 
SQL> SELECT  ID, NAME, AMOUNT, DATE   FROM CUSTOMERS   INNER JOIN 
ORDERS   ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID; 
+----+----------+--------+---------------------+ 
| ID | NAME     | AMOUNT | DATE                | 
+----+----------+--------+---------------------+ 
|  3 | kaushik  |   3000 | 2009-10-08 00:00:00 | 
|  3 | kaushik  |   1500 | 2009-10-08 00:00:00 | 
|  2 | Khilan   |   1560 | 2009-11-20 00:00:00 | 
|  4 | Chaitali |   2060 | 2008-05-20 00:00:00 | 
+----+----------+--------+---------------------+ 
LEFT JOIN 
SQL> SELECT  ID, NAME, AMOUNT, DATE   FROM CUSTOMERS   LEFT JOIN ORDERS  ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID; Output: 
+----+----------+--------+---------------------+ 
| ID | NAME     | AMOUNT | DATE                | 
+----+----------+--------+---------------------+ 
|  1 | Ramesh   |   NULL | NULL                | 
|  2 | Khilan   |   1560 | 2009-11-20 00:00:00 | 
|  3 | kaushik  |   3000 | 2009-10-08 00:00:00 | 
|  3 | kaushik  |   1500 | 2009-10-08 00:00:00 | 
|  4 | Chaitali |   2060 | 2008-05-20 00:00:00 | 
|  5 | Hardik   |   NULL | NULL                | 
|  6 | Komal    |   NULL | NULL                | 
|  7 | Muffy    |   NULL | NULL                | 
+----+----------+--------+---------------------+ RIGHT JOIN 
SQL> SELECT  ID, NAME, AMOUNT, DATE   FROM CUSTOMERS   RIGHT JOIN ORDERS   ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID; 
Output: 
+------+----------+--------+---------------------+ 
| ID   | NAME     | AMOUNT | DATE                | 
+------+----------+--------+---------------------+ 
|    3 | kaushik  |   3000 | 2009-10-08 00:00:00 | 
|    3 | kaushik  |   1500 | 2009-10-08 00:00:00 | 
|    2 | Khilan   |   1560 | 2009-11-20 00:00:00 | 
|    4 | Chaitali |   2060 | 2008-05-20 00:00:00 | 
+------+----------+--------+---------------------+ FULL JOIN  
SQL> SELECT  ID, NAME, AMOUNT, DATE   FROM CUSTOMERS   FULL JOIN ORDERS   ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID; 
Output: 
+------+----------+--------+---------------------+ 
| ID   | NAME     | AMOUNT | DATE                | 
+------+----------+--------+---------------------+ 
|    1 | Ramesh   |   NULL | NULL                | 
|    2 | Khilan   |   1560 | 2009-11-20 00:00:00 | 
|    3 | kaushik  |   3000 | 2009-10-08 00:00:00 | 
|    3 | kaushik  |   1500 | 2009-10-08 00:00:00 | 
|    4 | Chaitali |   2060 | 2008-05-20 00:00:00 | 
|    5 | Hardik   |   NULL | NULL                | 
|    6 | Komal    |   NULL | NULL                | 
|    7 | Muffy    |   NULL | NULL                | 
|    3 | kaushik  |   3000 | 2009-10-08 00:00:00 | 
|    3 | kaushik  |   1500 | 2009-10-08 00:00:00 | 
|    2 | Khilan   |   1560 | 2009-11-20 00:00:00 | 
|    4 | Chaitali |   2060 | 2008-05-20 00:00:00 | 
+------+----------+--------+---------------------+ SELF JOIN: 
SQL> SELECT  a.ID, b.NAME, a.SALARY    FROM CUSTOMERS a, CUSTOMERS b    WHERE a.SALARY < b.SALARY; 
Output: 
+----+----------+---------+ 
| ID | NAME     | SALARY  | 
+----+----------+---------+ 
|  2 | Ramesh   | 1500.00 | 
|  2 | kaushik  | 1500.00 | 
|  1 | Chaitali | 2000.00 | 
|  2 | Chaitali | 1500.00 | 
|  3 | Chaitali | 2000.00 | 
|  6 | Chaitali | 4500.00 | 
|  1 | Hardik   | 2000.00 | 
|  2 | Hardik   | 1500.00 | 
|  3 | Hardik   | 2000.00 | 
|  4 | Hardik   | 6500.00 | 
|  6 | Hardik   | 4500.00 | 
|  1 | Komal    | 2000.00 | 
|  2 | Komal    | 1500.00 | 
|  3 | Komal    | 2000.00 | 
|  1 | Muffy    | 2000.00 | 
|  2 | Muffy    | 1500.00 | 
|  3 | Muffy    | 2000.00 | 
|  4 | Muffy    | 6500.00 | 
|  5 | Muffy    | 8500.00 | 
|  6 | Muffy    | 4500.00 | 
+----+----------+---------+ 

