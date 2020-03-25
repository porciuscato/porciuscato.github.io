---
comments: true
title: sql command 모음
published: 2020-3-24
updated: 2020-3-24
tags: [sql]
categories: [development]
---

SQL 커맨드 모음



[링크](https://www.w3schools.com/sql/exercise.asp?filename=exercise_functions1)

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
  SELECT MIN(column_name)
  FROM table_name
  WHERE condition;
  ```

- `MAX()`: 최대값

  ```sql
  SELECT MAX(column_name)
  FROM table_name
  WHERE condition;
  ```

- `COUNT()`: 특정 칼럼의 row 갯수

  ```sql
  SELECT COUNT(column_name)
  FROM table_name
  WHERE condition;
  ```

- `AVG()`: 특정 칼럼 row 값들의 평균

  ```sql
  SELECT AVG(column_name)
  FROM table_name
  WHERE condition;
  ```

- `SUM()` : 특정 칼럼 row 값들의 합

  ```sql
  SELECT SUM(column_name)
  FROM table_name
  WHERE condition;
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

  