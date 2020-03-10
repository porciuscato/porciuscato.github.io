---
comments: true
title: ORACLE SQL의 데이터 타입에 대해 알아보자
published: false
updated: 2020-3-10
tags: [sql, oracle]
categories: [development]
---

ORACLE SQL의 데이터 타입에 대해 알아보자.



## SQL 데이터 타입

<center><img src="/assets/images/sql/sql-data-types.png" width="60%" style="margin: 0px auto;"></center>

> 출처: [JounarlDev](https://www.journaldev.com/16774/sql-data-types)

- DB 마다 지원하는 타입이 다르므로 확인하고 사용할 것
- 모든 데이터 타입을 표시하고 있지 않음. 다만 유명하고 자주 쓰이는 것 위주임



## Oracle Bulit-in Date Types

오라클에서 제공하는 데이터 타입에는 여러 가지가 있다. 

<font size='2'>- Oracle Built-in Data Types</font>

<font size='2'>- ANSI, DB2, and SQL/DS Date Types</font>

<font size='2'>- User-Defined Types</font>

<font size='2'>- Data Type Comparison Rules</font>

<font size='2'>- Data Conversion</font>

이 중 빌트인 타입에 대해 알아보자

빌트타입은 크게 4가지 형식으로 볼 수 있다. 이들은 명칭이라기 보다 범주다.

- Character 형식
- Numeric 형식
- Date 형식
- LOB 형식

## 문자 표현 자료형

CHAR / VARCHAR / TEXT

- CHAR [(size [BYTE | CHAR])]

  - 1 size는 1 byte다.

  - 이는 고정길이 데이터다. 가령 사이즈 10 byte를 선언하고 실제 입력된 데이터는 오직 2 byte만을 사용해도 10 byte를 온전히 사용한다.

- VARCHAR [(size [BYTE | CHAR])]

  - 가변길이 데이터다. CHAR와는 다르게 입력된 값에 따라 사이즈가 달라진다. 다만 최대치를 설정할 수 있다.
  - CHAR, VARCHAR 최대길이는 DB에 따라 다르다.

- NCHAR [(size)]

  - national character를 의미한다. CHAR의 UTF-8 인코딩과 같다.

  - 다음의 코드들은 모두 같다.

    ```sql
    CHAR(10) CHARACTER SET utf8
    NATIONAL CHARACTER(10)
    NCHAR(10)
    ```

- NVARCHAR

  - NCHAR의 가변길이형이다.

- TEXT
  - 가변길이형이다.





#### 참고

- [newLecture](https://www.youtube.com/watch?v=pGlkIFrY9QY&list=PLq8wAnVUcTFVq7RD1kuUwkdWabxvDGzfu)
- [GeeksforGeeks](https://www.geeksforgeeks.org/sql-ddl-dql-dml-dcl-tcl-commands/)
- [JounarlDev](https://www.journaldev.com/16774/sql-data-types)

