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
- [function](#function)
- [like](like)



## select

- customers 테이블에서 모든 것 가져오기

  ```sql
  select * from customers;
  ```

- customers에서 city 칼럼 가져오기 (여러 칼럼을 가져오려면 `,` comma로 구분)

  ```sql
  select city from customers;
  ```

```sql
select distinct city from customers;
```

- 중복없이 가져오기

  

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
  SELECT column_names
  FROM table_name
  WHERE column_name IS NULL;
  ```

- `IS NOT NULL`: 널이 아닐 경우

  ```sql
  SELECT column_names
  FROM table_name
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

  



