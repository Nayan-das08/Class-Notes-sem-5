# DBMS Lab Assignment Question 2
## Database Schema
| Entity   | Attributes                        |
| -------- | --------------------------------- |
| Supplier | (SNO, SNAME, STATUS, CITY)        | 
| Parts    | (PNO, PNAME, COLOR, WEIGHT, CITY) |
| Project  | (JNO, JNAME, CITY)                |
| SPJ      | (SNO, PNO, JNO, QTY)              |

```plain
CREATE TABLE supplier_0148
(
  sno     char(4)     PRIMARY KEY,
  sname   varchar(20) NOT NULL,
  status  varchar(10) NOT NULL,
  city    varchar(20) NOT NULL
);
```
---
```plain
CREATE TABLE parts_0148
(
  pno     char(4)     PRIMARY KEY,
  pname   varchar(20) NOT NULL,
  color   varchar(10),
  weight  integer NOT NULL,
  city    varchar(20) NOT NULL
);
```
---
```plain
CREATE TABLE project_0148
(
  jno   char(4)     PRIMARY KEY,
  jname varchar(20) NOT NULL,
  city  varchar(20) NOT NULL
);
```
---
```plain
CREATE TABLE spj_0148
(
  sno char(4) NOT NULL,
  pno char(4) NOT NULL,
  jno char(4) NOT NULL,
  qty char(4) NOT NULL,
  FOREIGN KEY (sno) REFERENCES supplier_0148(sno),
  FOREIGN KEY (pno) REFERENCES parts_0148(pno),
  FOREIGN KEY (jno) REFERENCES project_0148(jno)  
);
```
---

## Insert values in the database
```plain
INSERT INTO supplier_0148 VALUES
("S001", "supp_1", "ACTIVE", "Delhi"),
("S002", "supp_2", "INACTIVE", "Chennai"),
("S003", "supp_3", "INACTIVE", "Chennai"),
("S004", "supp_4", "INACTIVE", "Delhi"),
("S005", "supp_5", "ACTIVE", "Delhi"),
("S006", "supp_6", "ACTIVE", "Delhi"),
("S007", "supp_7", "ACTIVE", "London"),
("S008", "supp_8", "ACTIVE", "London"),
("S009", "supp_9", "INACTIVE", "Cape Town"),
("S010", "supp_10", "ACTIVE", "Chennai"),
("S011", "supp_11", "ACTIVE", "Chennai"),
("S012", "supp_12", "INACTIVE", "NYC"),
("S013", "supp_13", "ACTIVE", "Delhi"),
("S014", "supp_14", "INACTIVE", "NYC"),
("S015", "supp_15", "ACTIVE", "London");

INSERT INTO parts_0148 VALUES
("P001", "part_1", "Yellow", 12, "Cape Town"),
("P002", "part_2", "Black", 4, "NYC"),
("P003", "part_3", "White", 20, "NYC"),
("P004", "part_4", "Red", 11, "NYC"),
("P005", "part_5", "Black", 6, "Dubai"),
("P006", "part_6", "White", 16, "Cape Town"),
("P007", "part_7", "Purple", 4, "Chennai"),
("P008", "part_8", "Green", 1, "Dubai"),
("P009", "part_9", "Black", 12, "London"),
("P010", "part_10", "Blue", 1, "Delhi"),
("P011", "part_11", "Blue", 18, "Kyoto"),
("P012", "part_12", "Green", 13, "Chennai"),
("P013", "part_13", "Green", 4, "Kyoto"),
("P014", "part_14", "White", 10, "Kyoto"),
("P015", "part_15", "Black", 3, "Dubai");

INSERT INTO project_0148 VALUES
("J001", "project_1", "Cape Town"),
("J002", "project_2", "Kyoto"),
("J003", "project_3", "Chennai"),
("J004", "project_4", "NYC"),
("J005", "project_5", "Kyoto"),
("J006", "project_6", "London"),
("J007", "project_7", "Delhi"),
("J008", "project_8", "Kyoto"),
("J009", "project_9", "London"),
("J010", "project_10", "Delhi"),
("J011", "project_11", "Cape Town"),
("J012", "project_12", "NYC"),
("J013", "project_13", "Cape Town"),
("J014", "project_14", "Chennai"),
("J015", "project_15", "Kyoto");

INSERT INTO spj_0148 VALUES
("S001", "P009", "J002", 5),
("S002", "P013", "J002", 29),
("S012", "P012", "J009", 2),
("S007", "P007", "J002", 19),
("S008", "P013", "J005", 23),
("S012", "P001", "J002", 25),
("S004", "P014", "J004", 19),
("S014", "P005", "J009", 16),
("S008", "P002", "J006", 13),
("S010", "P010", "J014", 19),
("S013", "P008", "J001", 18),
("S006", "P006", "J013", 26),
("S010", "P012", "J011", 22),
("S006", "P009", "J006", 2),
("S015", "P005", "J013", 9),
("S002", "P001", "J001", 17),
("S014", "P001", "J001", 13),
("S007", "P015", "J007", 26),
("S009", "P014", "J014", 4),
("S014", "P011", "J014", 14),
("S010", "P002", "J012", 21),
("S012", "P011", "J003", 6),
("S013", "P005", "J013", 2),
("S006", "P012", "J004", 19),
("S014", "P003", "J002", 10),
("S011", "P005", "J010", 24),
("S014", "P002", "J012", 16),
("S010", "P012", "J007", 26),
("S002", "P003", "J010", 8),
("S012", "P007", "J015", 24),
("S014", "P006", "J007", 7),
("S002", "P014", "J008", 8),
("S005", "P010", "J006", 29),
("S009", "P015", "J015", 17),
("S007", "P013", "J007", 8),
("S012", "P002", "J014", 1),
("S015", "P001", "J009", 2),
("S001", "P013", "J006", 26),
("S009", "P009", "J014", 19),
("S006", "P005", "J007", 18),
("S011", "P013", "J012", 21),
("S011", "P013", "J012", 5),
("S003", "P008", "J004", 7),
("S008", "P015", "J012", 23),
("S007", "P007", "J003", 15),
("S008", "P015", "J013", 28),
("S002", "P014", "J011", 17),
("S008", "P014", "J013", 22),
("S004", "P005", "J015", 12),
("S005", "P015", "J002", 21);
```
---

## Queries
1.  Get sno values for suppliers who supply project J001. 

```plain
SELECT sno FROM spj_0148
WHERE jno = "J001";
```

```plain
mysql> SELECT sno FROM spj_0148
    -> WHERE jno = "J001";
+------+
| sno  |
+------+
| S013 |
| S002 |
| S014 |
+------+
3 rows in set (0.00 sec)
```
----------------------------------------------------
2.  Get sno values for suppliers who supply project J001 with part P001. 

```plain
SELECT sno FROM spj_0148
WHERE jno = "J001"
AND pno = "P001";
```

```plain
mysql> SELECT sno FROM spj_0148
    -> WHERE jno = "J001"
    -> AND pno = "P001";
+------+
| sno  |
+------+
| S002 |
| S014 |
+------+
2 rows in set (0.12 sec)
```
----------------------------------------------------
3.  Get jname values for projects supplied by supplier S001. 

```plain
SELECT spj_0148.*, project_0148.jname FROM spj_0148, project_0148
WHERE spj_0148.jno = project_0148.jno
AND sno = "S001";
```

```plain
mysql> SELECT spj_0148.*, project_0148.jname FROM spj_0148, project_0148
    -> WHERE spj_0148.jno = project_0148.jno
    -> AND sno = "S001";
+------+------+------+-----+-----------+
| sno  | pno  | jno  | qty | jname     |
+------+------+------+-----+-----------+
| S001 | P009 | J002 |   5 | project_2 |
| S001 | P013 | J006 |  26 | project_6 |
+------+------+------+-----+-----------+
2 rows in set (0.00 sec)
```
----------------------------------------------------
4.  Get color values for parts supplied by supplier S001. 

```plain
SELECT spj_0148.sno, parts_0148.color FROM spj_0148, parts_0148
WHERE spj_0148.pno = parts_0148.pno
AND sno = "S001";
```

```plain
mysql> SELECT spj_0148.sno, parts_0148.color FROM spj_0148, parts_0148
    -> WHERE spj_0148.pno = parts_0148.pno
    -> AND sno = "S001";
+------+-------+
| sno  | color |
+------+-------+
| S001 | Black |
| S001 | Green |
+------+-------+
2 rows in set (0.00 sec)
```
----------------------------------------------------
5.  Get pno values for parts supplied to any project in London. 

```plain
SELECT spj_0148.pno, project_0148.city FROM spj_0148, project_0148
WHERE spj_0148.jno = project_0148.jno
AND project_0148.city = "London";
```

```plain
mysql> SELECT spj_0148.pno, project_0148.city FROM spj_0148, project_0148
    -> WHERE spj_0148.jno = project_0148.jno
    -> AND project_0148.city = "London";
+------+--------+
| pno  | city   |
+------+--------+
| P002 | London |
| P009 | London |
| P010 | London |
| P013 | London |
| P012 | London |
| P005 | London |
| P001 | London |
+------+--------+
7 rows in set (0.00 sec)
```
----------------------------------------------------
6.  Get sno values for suppliers who supply project J001 with a yellow part. 

```plain
SELECT spj_0148.sno, spj_0148.jno, parts_0148.color FROM spj_0148, parts_0148
WHERE spj_0148.pno = parts_0148.pno
AND spj_0148.jno = "J001"
AND parts_0148.color = "Yellow";
```

```plain
mysql> SELECT spj_0148.sno, spj_0148.jno, parts_0148.color FROM spj_0148, parts_0148
    -> WHERE spj_0148.pno = parts_0148.pno
    -> AND spj_0148.jno = "J001"
    -> AND parts_0148.color = "Yellow";
+------+------+--------+
| sno  | jno  | color  |
+------+------+--------+
| S002 | J001 | Yellow |
| S014 | J001 | Yellow |
+------+------+--------+
2 rows in set (0.00 sec)
```
----------------------------------------------------
7.  Get sno values for suppliers who supply a London or NYC project with a black part. 

```plain
SELECT spj_0148.sno, project_0148.city, parts_0148.color 
FROM spj_0148, project_0148, parts_0148
WHERE spj_0148.jno = project_0148.jno
AND spj_0148.pno = parts_0148.pno
AND (project_0148.city = "London" OR project_0148.city = "NYC")
AND parts_0148.color = "Black";
```

```plain
mysql> SELECT spj_0148.sno, project_0148.city, parts_0148.color
    -> FROM spj_0148, project_0148, parts_0148
    -> WHERE spj_0148.jno = project_0148.jno
    -> AND spj_0148.pno = parts_0148.pno
    -> AND (project_0148.city = "London" OR project_0148.city = "NYC")
    -> AND parts_0148.color = "Black";
+------+--------+-------+
| sno  | city   | color |
+------+--------+-------+
| S008 | London | Black |
| S010 | NYC    | Black |
| S014 | NYC    | Black |
| S014 | London | Black |
| S006 | London | Black |
| S008 | NYC    | Black |
+------+--------+-------+
6 rows in set (0.00 sec)
```
----------------------------------------------------
8.  Get pno values for parts supplied to any project by a supplier in the same city. 

```plain
SELECT spj_0148.pno, project_0148.city AS "project.city",
supplier_0148.city AS "supplier.city" 
FROM spj_0148, project_0148, supplier_0148
WHERE spj_0148.jno = project_0148.jno
AND spj_0148.sno = supplier_0148.sno
AND project_0148.city = supplier_0148.city;
```

```plain
mysql> SELECT spj_0148.pno, project_0148.city AS "project.city",
    -> supplier_0148.city AS "supplier.city"
    -> FROM spj_0148, project_0148, supplier_0148
    -> WHERE spj_0148.jno = project_0148.jno
    -> AND spj_0148.sno = supplier_0148.sno
    -> AND project_0148.city = supplier_0148.city;
+------+--------------+---------------+
| pno  | project.city | supplier.city |
+------+--------------+---------------+
| P002 | London       | London        |
| P005 | Delhi        | Delhi         |
| P001 | London       | London        |
| P002 | NYC          | NYC           |
| P010 | Chennai      | Chennai       |
+------+--------------+---------------+
5 rows in set (0.00 sec)
```
----------------------------------------------------
9.  Get pno values for parts supplied to any project in London by a supplier in London. 

```plain
SELECT spj_0148.pno, project_0148.city AS "project.city", 
supplier_0148.city AS "supplier.city"
FROM spj_0148, project_0148, supplier_0148
WHERE spj_0148.jno = project_0148.jno
AND spj_0148.sno = supplier_0148.sno
AND project_0148.city = "London"
AND supplier_0148.city = "London";
```

```plain
mysql> SELECT spj_0148.pno, project_0148.city AS "project.city",
    -> supplier_0148.city AS "supplier.city"
    -> FROM spj_0148, project_0148, supplier_0148
    -> WHERE spj_0148.jno = project_0148.jno
    -> AND spj_0148.sno = supplier_0148.sno
    -> AND project_0148.city = "London"
    -> AND supplier_0148.city = "London";
+------+--------------+---------------+
| pno  | project.city | supplier.city |
+------+--------------+---------------+
| P002 | London       | London        |
| P001 | London       | London        |
+------+--------------+---------------+
2 rows in set (0.00 sec)
```
----------------------------------------------------
10. Get jno values for projects supplied by at least one supplier not in the same city. 

```plain
SELECT spj_0148.jno, project_0148.city AS "project.city",
supplier_0148.city AS "supplier.city" 
FROM spj_0148, supplier_0148, project_0148
WHERE spj_0148.sno = supplier_0148.sno
AND spj_0148.jno = project_0148.jno
AND supplier_0148.city <> project_0148.city
ORDER BY spj_0148.jno;
```

```plain
mysql> SELECT spj_0148.jno, project_0148.city AS "project.city",
    -> supplier_0148.city AS "supplier.city"
    -> FROM spj_0148, supplier_0148, project_0148
    -> WHERE spj_0148.sno = supplier_0148.sno
    -> AND spj_0148.jno = project_0148.jno
    -> AND supplier_0148.city <> project_0148.city
    -> ORDER BY spj_0148.jno;
+------+--------------+---------------+
| jno  | project.city | supplier.city |
+------+--------------+---------------+
| J001 | Cape Town    | Chennai       |
| J001 | Cape Town    | NYC           |
| J001 | Cape Town    | Delhi         |
| J002 | Kyoto        | Delhi         |
| J002 | Kyoto        | Chennai       |
| J002 | Kyoto        | NYC           |
| J002 | Kyoto        | Delhi         |
| J002 | Kyoto        | London        |
| J002 | Kyoto        | NYC           |
| J003 | Chennai      | NYC           |
| J003 | Chennai      | London        |
| J004 | NYC          | Chennai       |
| J004 | NYC          | Delhi         |
| J004 | NYC          | Delhi         |
| J005 | Kyoto        | London        |
| J006 | London       | Delhi         |
| J006 | London       | Delhi         |
| J006 | London       | Delhi         |
| J007 | Delhi        | London        |
| J007 | Delhi        | London        |
| J007 | Delhi        | Chennai       |
| J007 | Delhi        | NYC           |
| J008 | Kyoto        | Chennai       |
| J009 | London       | NYC           |
| J009 | London       | NYC           |
| J010 | Delhi        | Chennai       |
| J010 | Delhi        | Chennai       |
| J011 | Cape Town    | Chennai       |
| J011 | Cape Town    | Chennai       |
| J012 | NYC          | Chennai       |
| J012 | NYC          | Chennai       |
| J012 | NYC          | London        |
| J012 | NYC          | Chennai       |
| J013 | Cape Town    | London        |
| J013 | Cape Town    | London        |
| J013 | Cape Town    | Delhi         |
| J013 | Cape Town    | Delhi         |
| J013 | Cape Town    | London        |
| J014 | Chennai      | Cape Town     |
| J014 | Chennai      | Cape Town     |
| J014 | Chennai      | NYC           |
| J014 | Chennai      | NYC           |
| J015 | Kyoto        | NYC           |
| J015 | Kyoto        | Delhi         |
| J015 | Kyoto        | Cape Town     |
+------+--------------+---------------+
45 rows in set (0.00 sec)
```
----------------------------------------------------
11. Get all pairs of city values such that a supplier in the first city supplies a project in the second city. 

```plain
SELECT DISTINCT supplier_0148.city AS "supplier.city",
project_0148.city AS "project.city"
FROM spj_0148, supplier_0148, project_0148
WHERE spj_0148.jno = project_0148.jno
AND spj_0148.sno = supplier_0148.sno;
```

```plain
mysql> SELECT DISTINCT supplier_0148.city AS "supplier.city",
    -> project_0148.city AS "project.city"
    -> FROM spj_0148, supplier_0148, project_0148
    -> WHERE spj_0148.jno = project_0148.jno
    -> AND spj_0148.sno = supplier_0148.sno;
+---------------+--------------+
| supplier.city | project.city |
+---------------+--------------+
| Delhi         | Kyoto        |
| Delhi         | London       |
| Chennai       | Kyoto        |
| Chennai       | Cape Town    |
| Chennai       | Delhi        |
| Chennai       | NYC          |
| Delhi         | NYC          |
| Delhi         | Cape Town    |
| Delhi         | Delhi        |
| London        | Kyoto        |
| London        | Delhi        |
| London        | Chennai      |
| London        | London       |
| London        | NYC          |
| London        | Cape Town    |
| Cape Town     | Chennai      |
| Cape Town     | Kyoto        |
| Chennai       | Chennai      |
| NYC           | London       |
| NYC           | Kyoto        |
| NYC           | Chennai      |
| NYC           | Cape Town    |
| NYC           | NYC          |
| NYC           | Delhi        |
+---------------+--------------+
24 rows in set (0.04 sec)
```
----------------------------------------------------
13. Get pno values for parts supplied to all projects in London. 

```plain
SELECT spj_0148.pno, project_0148.jno, project_0148.city FROM spj_0148, project_0148
WHERE spj_0148.jno = project_0148.jno
AND project_0148.city = "London";
```

```plain
mysql> SELECT spj_0148.pno, project_0148.jno, project_0148.city FROM spj_0148, project_0148
    -> WHERE spj_0148.jno = project_0148.jno
    -> AND project_0148.city = "London";
+------+------+--------+
| pno  | jno  | city   |
+------+------+--------+
| P002 | J006 | London |
| P009 | J006 | London |
| P010 | J006 | London |
| P013 | J006 | London |
| P012 | J009 | London |
| P005 | J009 | London |
| P001 | J009 | London |
+------+------+--------+
7 rows in set (0.00 sec)
```
----------------------------------------------------
14. Get sname values for suppliers who supplies at least one green part to any project. 

```plain
SELECT supplier_0148.sname, parts_0148.color, spj_0148.jno 
FROM spj_0148, parts_0148, supplier_0148
WHERE spj_0148.pno = parts_0148.pno
AND spj_0148.sno = supplier_0148.sno
AND parts_0148.color = "Green";
```

```plain
mysql> SELECT supplier_0148.sname, parts_0148.color, spj_0148.jno
    -> FROM spj_0148, parts_0148, supplier_0148
    -> WHERE spj_0148.pno = parts_0148.pno
    -> AND spj_0148.sno = supplier_0148.sno
    -> AND parts_0148.color = "Green";
+---------+-------+------+
| sname   | color | jno  |
+---------+-------+------+
| supp_13 | Green | J001 |
| supp_3  | Green | J004 |
| supp_12 | Green | J009 |
| supp_10 | Green | J011 |
| supp_6  | Green | J004 |
| supp_10 | Green | J007 |
| supp_2  | Green | J002 |
| supp_8  | Green | J005 |
| supp_7  | Green | J007 |
| supp_1  | Green | J006 |
| supp_11 | Green | J012 |
| supp_11 | Green | J012 |
+---------+-------+------+
12 rows in set (0.00 sec)
```
----------------------------------------------------
15. Get total quantity of part P014 supplied by supplier S002. 

```plain
SELECT sum(qty) AS "qty of P014 supplied by S002" FROM 
(SELECT sno, pno, qty FROM spj_0148 
WHERE sno = "S002" 
AND pno = "P014") qty_p14_s2;
```

```plain
mysql> SELECT sum(qty) AS "qty of P014 supplied by S002" FROM
    -> (SELECT sno, pno, qty FROM spj_0148
    -> WHERE sno = "S002"
    -> AND pno = "P014") qty_p14_s2;
+------------------------------+
| qty of P014 supplied by S002 |
+------------------------------+
|                           25 |
+------------------------------+
1 row in set (0.04 sec)
```
----------------------------------------------------
16. Get the total number of projects supplied by supplier S003. 

```plain
SELECT count(*) FROM spj_0148 WHERE sno = "S003";
```

```plain
mysql> SELECT count(*) FROM spj_0148 WHERE sno = "S003";
+----------+
| count(*) |
+----------+
|        1 |
+----------+
1 row in set (0.00 sec)
```
----------------------------------------------------
17. Change colour of all red parts to orange. 

```plain
UPDATE parts_0148
SET color = "Orange"
WHERE color = "Red";
```
----------------------------------------------------
18. Get sname values for suppliers who supply to both projects J001 and J002. 

```plain
SELECT j1.sno FROM
(SELECT sno, jno FROM spj_0148 WHERE jno = "J001") j1,
(SELECT sno, jno FROM spj_0148 WHERE jno = "J002") j2
WHERE j1.sno = j2.sno;

SELECT j1.sno FROM
(SELECT sno, jno FROM spj_0148 WHERE jno = "J001") j1
INNER JOIN
(SELECT sno, jno FROM spj_0148 WHERE jno = "J002") j2
ON j1.sno = j2.sno;

select sno from 
(select sno, jno from spj_0148 where jno = "J001") j1
WHERE sno IN
(select sno from spj_0148 where jno = "J002");
```

```plain
+------+
| sno  |
+------+
| S002 |
| S014 |
+------+
2 rows in set (0.00 sec)
```
----------------------------------------------------
19. Get all city, pno, city triples such that a supplier in the first city supplies the specified part to a project in the second city. 

```plain
SELECT DISTINCT supplier_0148.city AS "supplier.city",
parts_0148.pno,
project_0148.city AS "project.city"
FROM spj_0148, supplier_0148, project_0148, parts_0148
WHERE spj_0148.jno = project_0148.jno
AND spj_0148.sno = supplier_0148.sno
AND spj_0148.pno = parts_0148.pno;
```

```plain
mysql> SELECT DISTINCT supplier_0148.city AS "supplier.city",
    -> parts_0148.pno,
    -> project_0148.city AS "project.city"
    -> FROM spj_0148, supplier_0148, project_0148, parts_0148
    -> WHERE spj_0148.jno = project_0148.jno
    -> AND spj_0148.sno = supplier_0148.sno
    -> AND spj_0148.pno = parts_0148.pno;
+---------------+------+--------------+
| supplier.city | pno  | project.city |
+---------------+------+--------------+
| Delhi         | P009 | Kyoto        |
| Delhi         | P013 | London       |
| Chennai       | P013 | Kyoto        |
| Chennai       | P001 | Cape Town    |
| Chennai       | P003 | Delhi        |
| Chennai       | P014 | Kyoto        |
| Chennai       | P014 | Cape Town    |
| Chennai       | P008 | NYC          |
| Delhi         | P014 | NYC          |
| Delhi         | P005 | Kyoto        |
| Delhi         | P010 | London       |
| Delhi         | P015 | Kyoto        |
| Delhi         | P006 | Cape Town    |
| Delhi         | P009 | London       |
| Delhi         | P012 | NYC          |
| Delhi         | P005 | Delhi        |
| London        | P007 | Kyoto        |
| London        | P015 | Delhi        |
| London        | P013 | Delhi        |
| London        | P007 | Chennai      |
| London        | P013 | Kyoto        |
| London        | P002 | London       |
| London        | P015 | NYC          |
| London        | P015 | Cape Town    |
| London        | P014 | Cape Town    |
| Cape Town     | P014 | Chennai      |
| Cape Town     | P015 | Kyoto        |
| Cape Town     | P009 | Chennai      |
| Chennai       | P010 | Chennai      |
| Chennai       | P012 | Cape Town    |
| Chennai       | P002 | NYC          |
| Chennai       | P012 | Delhi        |
| Chennai       | P005 | Delhi        |
| Chennai       | P013 | NYC          |
| NYC           | P012 | London       |
| NYC           | P001 | Kyoto        |
| NYC           | P011 | Chennai      |
| NYC           | P007 | Kyoto        |
| NYC           | P002 | Chennai      |
| Delhi         | P008 | Cape Town    |
| Delhi         | P005 | Cape Town    |
| NYC           | P005 | London       |
| NYC           | P001 | Cape Town    |
| NYC           | P003 | Kyoto        |
| NYC           | P002 | NYC          |
| NYC           | P006 | Delhi        |
| London        | P005 | Cape Town    |
| London        | P001 | London       |
+---------------+------+--------------+
48 rows in set (0.00 sec)
```
----------------------------------------------------
20. Get jnames for those project which are supplied by supplier supp_2. 

```plain
SELECT project_0148.jname, supplier_0148.sname 
FROM spj_0148, supplier_0148, project_0148
WHERE spj_0148.sno = supplier_0148.sno
AND spj_0148.jno = project_0148.jno
AND supplier_0148.sname = "supp_2";
```

```plain
mysql> SELECT project_0148.jname, supplier_0148.sname
    -> FROM spj_0148, supplier_0148, project_0148
    -> WHERE spj_0148.sno = supplier_0148.sno
    -> AND spj_0148.jno = project_0148.jno
    -> AND supplier_0148.sname = "supp_2";
+------------+--------+
| jname      | sname  |
+------------+--------+
| project_2  | supp_2 |
| project_1  | supp_2 |
| project_10 | supp_2 |
| project_8  | supp_2 |
| project_11 | supp_2 |
+------------+--------+
5 rows in set (0.00 sec)
```
----------------------------------------------------
