---
comments: true
title: sql command 모음
published: false
updated: 2020-3-24
tags: [sql]
categories: [development]
---

SQL 커맨드 모음



[링크](https://www.w3schools.com/sql/default.asp)

# 차례

- [select](#select)
- [where](#where)
- [order by](#order by)
- [insert](insert)
- [Null Value](#Null Value)
- [update](#update)
- [delete](#delete)
- [function](#function) : Built-in function
- [like](#like)
- [wildcards](#wildcards)
- [in](#in)
- [between](#between)
- [aliases](#aliases)
- [joins](#joins)
- [union](#union)
- [group by](#group by)
- [having](#having)
- [exists](#exists)
- [any, all](#any, all)
- [select into](#select into)
- [insert into](#insert into)
- [case](#case)
- [null functions](#null functions)
- [stored procedures](#stored procedures)
- [comments](#comments)
- [limit](#limit)

#### Database

- [create](#create)
- [drop](#drop)
- [backup](#backup)
- [alter](#alter)



## select

- customers 테이블에서 모든 것 가져오기

  ```sql
  select * from customers;
  ```

- customers에서 city 칼럼 가져오기 (여러 칼럼을 가져오려면 `,` comma로 구분)

  ```sql
  select city from customers;
  ```

- 중복없이 가져오기

  ```sql
  select distinct city from customers;
  ```
  
  

## where

filtering

- `=, >, <, >=, <=` :여타 언어와 동일

- `<>, !=` : not equal

  - 이렇게도 쓸 수 있다.

    ```sql
    where not city = "Paris";
    where city != "Paris";
    ```

- `BETWEEN` : 사이

  ```sql
  BETWEEN 50 and 60;
  ```

- `WHERE` : 조건 검색

  ```sqlite
  where city like "Par_%";
  ```
  - `_` : single character
  - `%` : multiple character

- `and` or `or` : 여러 조건 검색

  ```sql
  where City = "Paris" and Code = 123;
  where City = "Paris" or City = "London";
  ```

- `IN` : 특정 칼럼의 여러 조건을 검색

  ```sql
  where City in ("Paris", "London")
  ```

  - 파리거나 런던이면 가져온다.



## order by

sorting. 특정 칼럼으로 가져오는 순서 설정

- `ASC` : 오름차순(default)

  ```sql
  SELECT * FROM Customers ORDER BY Country DESC;
  ```

- `DESC`: 내림차순

  ```sql
  SELECT * FROM Customers ORDER BY Country DESC;
  ```

- 여러 칼럼의 순서대로 가져오기

  ```sql
  SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;
  ```

  

## insert

테이블에 새 레코드 삽입

```sql
INSERT INTO table_name (column1, column2, column3, ...) 
VALUES (value1, value2, value3, ...);
```



## Null Value

- `IS NULL` : 널일 경우

  ```sql
  SELECT column_names FROM table_name
  WHERE column_name IS NULL;
  ```
  
- `IS NOT NULL`: 널이 아닐 경우

  ```sql
  SELECT column_names FROM table_name
  WHERE column_name IS NOT NULL;
  ```



## update

현재 존재하는 레코드의 정보를 수정

- 기본 문법

  ```sql
  UPDATE table_name
  SET column1 = value1, column2 = value2, ...
  WHERE condition;
  ```

  > where를 빼면 모든 레코드가 수정이 되니 조심하자



## delete

조건에 해당하는 레코드를 삭제

```sql
DELETE FROM table_name WHERE condition;
```

> where를 안 쓰면 테이블의 모든 row를 지운다.



## function

- `MIN()` : 최소값

  ```sql
  SELECT MIN(column_name) FROM table_name WHERE condition;
  ```
  
- `MAX()`: 최대값

  ```sql
  SELECT MAX(column_name) FROM table_name WHERE condition;
  ```
  
- `COUNT()`: 특정 칼럼의 row 갯수

  ```sql
  SELECT COUNT(column_name) FROM table_name WHERE condition;
  ```
  
- `AVG()`: 특정 칼럼 row 값들의 평균

  ```sql
  SELECT AVG(column_name) FROM table_name WHERE condition;
  ```
  
- `SUM()` : 특정 칼럼 row 값들의 합

  ```sql
  SELECT SUM(column_name) FROM table_name WHERE condition;
  ```



## like

패턴 검색

- 기본 문법

  ```sql
  SELECT * FROM Customers WHERE CustomerName LIKE '%or%';
  SELECT * FROM Customers WHERE CustomerName LIKE '_r%';
  ```

  - `_` : single character
  - `%` : multiple character

- 부정형

  ```sql
  SELECT * FROM Customers WHERE CustomerName NOT LIKE '%or%';
  ```

  

## wildcards

`LIKE`와 함께 쓰이며 character를 대체한다.

| Symbol | Description                                         | Example                                  |
| :----- | :-------------------------------------------------- | :--------------------------------------- |
| %      | Represents zero or more characters                  | bl% finds bl, black, blue, and blob      |
| _      | Represents a single character                       | h_t finds hot, hat, and hit              |
| []     | Represents any single character within the brackets | h[oa]t finds hot and hat, but not hit    |
| ^      | Represents any character not in the brackets        | `h[^oa]t` finds hit, but not hot and hat |
| -      | Represents a range of characters                    | c[a-b]t finds cat and cbt                |



## in

- 기본 문법

  ```sql
  SELECT column_name(s) FROM table_name
  WHERE column_name IN (value1, value2, ...);
  ```

- 부정형

  ```sql
  SELECT column_name(s) FROM table_name
  WHERE column_name NOT IN (value1, value2, ...);
  ```

- 다른 쿼리 조건에서도 가능

  ```sql
  SELECT * FROM Customers
  WHERE Country IN (SELECT Country FROM Suppliers);
  ```



##  between

selects values wihtin a given range

- 기본 문법

  ```sql
  SELECT column_name(s) FROM table_name
  WHERE column_name BETWEEN value1 AND value2;
  ```

- text도 가능하다.

  ```sql
  SELECT * FROM Products
  WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
  ORDER BY ProductName;
  ```

- 부정형

  ```sql
  SELECT * FROM Products
  WHERE ProductName NOT BETWEEN 'Carnarvon' AND 'Mozzarella'
  ORDER BY ProductName;
  ```

  

## aliases

별칭을 부여. column name이 아닌 alias로 결과가 나온다.

- 기본 문법

  ```sql
  SELECT column_name AS alias_name 
  FROM table_name;
  ```

- 2개 이상을 만들 때

  ```sql
  SELECT CustomerID AS ID, CustomerName AS Customer
  FROM Customers;
  ```

- alias가 2단어 이상일 때

  ```sql
  SELECT CustomerName AS Customer, ContactName AS [Contact Person]
  FROM Customers;
  ```

- 여러 칼럼을 하나의 칼럼으로 출력하고 싶을 때

  ```sql
  SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
  FROM Customers;
  ```

  => 칼럼이 CustomerName과 Address 2개로 나온다.

  `CONCAT()`을 쓸 수도 있다.

  ```sql
  SELECT CustomerName, CONCAT(Address,', ', PostalCode, ', ', City, ', ', Country) AS Address
  FROM Customers;
  ```



### 테이블 이름에 alias 사용하기

- 예시

  ```sql
  SELECT o.OrderID, o.OrderDate, c.CustomerName
  FROM Customers AS c, Orders AS o
  WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;
  ```

  Customers 테이블을 c, Orders 테이블을 o라 하여 쿼리를 짧게 만들었다.



## joins

관계있는 여러 테이블들에서 가져오는 형식

- 예시

  ```sql
  SELECT o.OrderID, c.CustomerName, o.OrderDate FROM Orders as o
  INNER JOIN Customers as c ON o.CustomerID = c.CustomerID;
  ```

- join의 종류

  | Join                   | Description                                                  |
  | ---------------------- | ------------------------------------------------------------ |
  | **(INNER) JOIN**       | Returns records that have matching values in both tables     |
  | **LEFT (OUTER) JOIN**  | Returns all records from the left table, and the matched records from the right table |
  | **RIGHT (OUTER) JOIN** | Returns all records from the right table, and the matched records from the left table |
  | **FULL (OUTER) JOIN**  | Returns all records when there is a match in either left or right table |

  > - from이 좌측 테이블, join이 우측 테이블이다.
  >
  > - 어떤 SQL 에서는 LEFT OUTER JOIN으로 써야한다.

  <center><img src="/assets/images/sql/sql_join.jpg" width="100%" style="margin: 0px auto;"></center>

### INNER JOIN

두 테이블 모두 조건을 충족하는 칼럼을 반환

- 예시

  ```sql
  SELECT column_name(s) FROM table1 INNER JOIN table2
  ON table1.column_name = table2.column_name;
  ```

- 3개 이상의 테이블에서 가져오기

  ```sql
  SELECT o.OrderID, c.CustomerName, s.ShipperName
  FROM (
  (Orders as o INNER JOIN Customers as c ON o.CustomerID = c.CustomerID)
  INNER JOIN Shippers as s ON o.ShipperID = s.ShipperID);
  ```

  o 와 c의 교집합을 구한 뒤, 그 결과와 s의 교집합을 구한다.
  
  - 4개 테이블에서 정보 가져오기
  
    ```sql
    SELECT O.OrderID, C.CustomerID, O.OrderDate, OD.ProductID, P.ProductName, P.Price, OD.Quantity 
    FROM ((
    (Orders as O join Customers as C on O.CustomerID = C.CustomerID)
    join OrderDetails as OD on O.OrderID = OD.OrderID)
    join Products as P on OD.ProductID = P.ProductID)
    where O.OrderID = 10250;
    ```
  
    

### LEFT JOIN

좌측 테이블의 모든 row와 조건에 맞는 우측 테이블의 row를 반환

- 예시

  ```sql
  SELECT column_name(s) FROM table1 LEFT JOIN table2
  ON table1.column_name = table2.column_name;
  ```

> RIGHT JOIN, FULL JOIN도 같은 문법 구조다. 논리는 위에 쓰여진 대로다.



### SELF JOIN

inner join과 같으나 테이블 하나에서 조인을 한다.

- 기본 문법

  ```sql
  SELECT column_name(s) FROM table1 T1, table1 T2
  WHERE condition;
  ```

  > T1과 T2는 모두 동일한 table1을 의미한다. self join은 AS를 사용하지 않는다.

- 예시

  ```sql
  SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City FROM Customers A, Customers B
  WHERE A.CustomerID <> B.CustomerID AND A.City = B.City 
  ORDER BY A.City;
  ```

  고객마다 같은 도시인 다른 고객들을 모두 나타낸다.



## union

The UNION operator is used to combine the result-set of two or more SELECT statements.

- 핵심 조건
  - Each SELECT statement within UNION must have the same number of columns
  - The columns must also have similar data types
  - The columns in each SELECT statement must also be in the same order

- 기본 문법

  ```sql
  SELECT a, b, c FROM table1
  UNION
  SELECT a, b, c FROM table2;
  ```

  기본적으로 distinct다. 모든 값을 가져오고 싶을 땐 `ALL`을 사용하자.

- `UNION ALL`

  ```sql
  SELECT a, b, c FROM table1
  UNION ALL
  SELECT a, b, c FROM table2;
  ```

- where 사용하기

  ```sql
  SELECT City, Country FROM Customers WHERE Country='Germany'
  UNION
  SELECT City, Country FROM Suppliers WHERE Country='Germany'
  ORDER BY City;
  ```

  distinct value만 가져오기 때문에 중복을 허용한다면 ALL을 쓰자.

- 칼럼 이름이 다르더라도 비슷한 형식이면 UNION을 사용할 수 있다.

  ```sql
  SELECT 'Customer' As Type, ContactName, City, Country FROM Customers
  UNION
  SELECT 'Supplier', ContactName, City, Country FROM Suppliers;
  ```

  

## group by

칼럼의 값이 같은 것들을 한 행으로 묶는다.

- 기본 문법

  ```sql
  SELECT column_name(s) FROM table_name WHERE condition
  GROUP BY column_name(s)
  ORDER BY column_name(s);
  ```

- 예시

  ```sql
  SELECT COUNT(CustomerID), Country FROM Customers
  GROUP BY Country ORDER BY COUNT(CustomerID) DESC;
  ```

  > Country가 같은 것들을 묶는다.
  >
  > 이때 각 행은 국가에 속한 ID의 수와 국가를 보여준다.



## having

where가 쓰일 수 없는 위치에서 having을 쓴다. 가령 group by의 뒤쪽

- 기본 문법

  ```sql
  SELECT column_name(s) FROM table_name WHERE condition
  GROUP BY column_name(s) HAVING condition
  ORDER BY column_name(s);
  ```

- 예시

  ```sql
  SELECT COUNT(CustomerID), Country FROM Customers 
  GROUP BY Country
  HAVING COUNT(CustomerID) > 5
  ORDER BY COUNT(CustomerID) DESC;
  ```

  

## exists

서브 쿼리를 확인하기 위해 쓰인다. 만약 하나 이상의 레코드가 있다면 True를 반환한다.

- 기본 문법

  ```sql
  SELECT column_name(s) FROM table_name
  WHERE EXISTS (SELECT column_name FROM table_name WHERE condition);
  ```

- 예시

  ```sql
  SELECT SupplierName FROM Suppliers
  WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);
  ```

  > exists의 조건을 만족하는 레코드가 하나 이상 있는 SupplierName을 반환한다.



## any, all

The ANY and ALL operators are used with a WHERE or HAVING clause.
The ANY operator returns true if any of the subquery values meet the condition.
The ALL operator returns true if all of the subquery values meet the condition.

- ANY 기본 문법

  ```sql
  SELECT column_name(s) FROM table_name
  WHERE column_name operator ANY
  (SELECT column_name FROM table_name WHERE condition);
  ```
  - 예시

    ```sql
    SELECT ProductName FROM Products
    WHERE ProductID = ANY (SELECT ProductID FROM OrderDetails WHERE Quantity > 99);
    ```

    > ANY 조건에 하나라도 부합하는 레코드가 있다면 True를 반환한다.

- ALL 기본 문법

  ```sql
  SELECT column_name(s) FROM table_name
  WHERE column_name operator ALL
  (SELECT column_name FROM table_name WHERE condition);
  ```

  - 예시

    ```sql
    SELECT ProductName FROM Products
    WHERE ProductID = ALL (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);
    ```

    > OrderDatails의 ProductID 칼럼이 모두 해당 조건을 만족해야만 True가 반환된다.



## select into

The SELECT INTO statement copies data from one table into a new table.

This makes a new table.

- Syntax

  ```sql
  SELECT * INTO newtable [IN externaldb]
  FROM oldtable WHERE condition;
  ```

  it is possible to insert many columns.

  ```sql
  SELECT column1, column2, column3, ... INTO newtable [IN externaldb]
  FROM oldtable WHERE condition;
  ```

- example

  Use `IN` to insert another database.

  ```sql
  SELECT * INTO CustomersBackup2020 IN 'Backup.mdb' FROM Customers;
  ```

- create a new empty table with a same schema of older one

  SELECT INTO can also be used to create a new, empty table using the schema of another. Just add a WHERE clause that causes the query **to return no data**

  ```sql
  SELECT * INTO newtable FROM oldtable WHERE 1 = 0;
  ```

  

## insert into

The INSERT INTO SELECT statement copies data from one table and inserts it into another table.

```
- INSERT INTO SELECT requires that data types in source and target tables match
- The existing records in the target table are unaffected
```

- Syntax

  ```sql
  INSERT INTO table2 SELECT * FROM table1 WHERE condition;
  ```

  Copy only some columns

  ```sql
  INSERT INTO table2 (column1, column2, column3, ...)
  SELECT column1, column2, column3, ...
  FROM table1 WHERE condition;
  ```

- example

  ```sql
  INSERT INTO Customers (CustomerName, City, Country)
  SELECT SupplierName, City, Country FROM Suppliers WHERE Country='Germany';
  ```

  

## case

The CASE statement goes through conditions and returns a value when the first condition is met **(like an IF-THEN-ELSE statement)**. So, once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in the ELSE clause.

If there is no ELSE part and no conditions are true, it returns NULL.

- Syntax

  ```sql
  CASE
      WHEN condition1 THEN result1
      WHEN condition2 THEN result2
      WHEN conditionN THEN resultN
      ELSE result
  END;
  ```

- example

  ```sql
  SELECT OrderID, Quantity,
  CASE
      WHEN Quantity > 30 THEN 'The quantity is greater than 30'
      WHEN Quantity = 30 THEN 'The quantity is 30'
      ELSE 'The quantity is under 30'
  END AS QuantityText
  FROM OrderDetails;
  ```

  result

  | OrderID | Quantity | QuantityText             |
  | :------ | :------- | :----------------------- |
  | 10248   | 12       | The quantity is under 30 |
  | 10248   | 10       | The quantity is under 30 |
  | 10248   | 5        | The quantity is under 30 |

- example 2

  ```sql
  SELECT OrderID, Quantity,
  CASE
      WHEN Quantity > 30 THEN 'The quantity is greater than 30'
      WHEN Quantity = 30 THEN 'The quantity is 30'
      ELSE 'The quantity is under 30'
  END
  FROM OrderDetails;
  ```

  result

  | OrderID | Quantity | CASE WHEN Quantity > 30 THEN 'The quantity is greater than 30' WHEN Quantity = 30 THEN 'The quantity is 30' ELSE 'The quantity is under 30' END |
  | :------ | :------- | :----------------------------------------------------------- |
  | 10248   | 12       | The quantity is under 30                                     |
  | 10248   | 10       | The quantity is under 30                                     |

  > Use `AS` as possible as you can.

- **Check this example out!**

  ```sql
  SELECT CustomerName, City, Country
  FROM Customers
  ORDER BY
  (CASE
      WHEN City IS NULL THEN Country
      ELSE City
  END);
  ```



## null functions

- **IFNULL()**

  - example

    ```sql
    SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))
    FROM Products;
    ```

    if UnitsOnOder is null, return 0 otherwise return UnitsOnOrder

- **ISNULL()**

  - example

    ```sql
    SELECT ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0))
    FROM Products;
    ```

    same with IFNULL()

- **COALESCE()**

  - example

    ```sql
    SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
    FROM Products;
    ```

    return the first non-null value on list

- **NVL()**

  - example

    ```sql
    SELECT ProductName, UnitPrice * (UnitsInStock + NVL(UnitsOnOrder, 0))
    FROM Products;
    ```

    This is for Oracle DB.

    

## stored procedures

&nbsp;&nbsp;A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.
&nbsp;&nbsp;So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it.
&nbsp;&nbsp;You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed.

- Stored Procedure Syntax

  ```sql
  CREATE PROCEDURE procedure_name
  AS
  sql_statement
  GO;
  ```

- Execute Procedure Syntax

  ```sql
  EXEC procedure_name;
  ```

  - example

    ```sql
    CREATE PROCEDURE SelectAllCustomers
    AS
    SELECT * FROM Customers
    GO;
    
    EXEC SelectAllCustomers;
    ```

- You can create procedures with **Parameters**.

  - One param

    ```sql
    CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
    AS
    SELECT * FROM Customers WHERE City = @City
    GO;
    
    EXEC SelectAllCustomers @City = 'London';
    ```

  - More than Two param

    ```sql
    CREATE PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
    AS
    SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
    GO;
    
    EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP';
    ```



## comments

- Single line

  ```sql
  --Select all:
  ```

- Multi line

  ```sql
  /*Select all the columns
  of all the records
  in the Customers table:*/
  ```

  

### limit

used to specify the number of records to return

- example

  ```sql
  SELECT * FROM Customers LIMIT 3;
  ```

  상위 3개만 반환

- `SELECT TOP`

  ```sql
  SELECT TOP 3 * FROM Customers;
  ```

  > same as upper.
  >
  > not all databases support SELECT TOP

- `ROWNUM` : Oracle

  ```sql
  SELECT * FROM Customers WHERE ROWNUM <= 3;
  ```

  

---

## Database

### create

데이터베이스, 테이블 생성하는 명령어다.

- Syntax Database

  ```sql
  CREATE DATABASE databasename;
  ```
  
- Syntax Table

  ```sql
  CREATE TABLE table_name (
      column1 datatype,
      column2 datatype,
      column3 datatype,
     ....
  );
  ```

  - example

    ```sql
    CREATE TABLE Persons (
        PersonID int,
        LastName varchar(255),
        FirstName varchar(255),
        Address varchar(255),
        City varchar(255)
    );
    ```

    

### drop

- Syntax Database

  ```sql
  DROP DATABASE databasename;
  ```


- Syntax Table

  ```sql
  DROP TABLE Shippers;
  ```

  



### backup

The BACKUP DATABASE statement is used in SQL Server to create a full back up of an existing SQL database.

- Syntax

  ```sql
  BACKUP DATABASE databasename
  TO DISK = 'filepath'
  WITH DIFFERENTIAL;
  ```

- Example

  ```sql
  BACKUP DATABASE testDB
  TO DISK = 'D:\backups\testDB.bak';
  ```

  D 드라이브 위치에 저장한다.



### alter

- Syntax

  ```sql
  ALTER TABLE table_name
  ADD column_name datatype;
  ```

  - example

    ```sql
    ALTER TABLE Customers ADD Email varchar(255);
    ```