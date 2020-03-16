---
comments: true
title: Dump Data를 mariaDB에 넣기
published: false
updated: 2020-3-16
tags: [sql, dump, mariaDB]
categories: [development]
---

CSV, txt 형식으로된 데이터를 mariaDB에 넣자.



# Dump Data를 DB에 넣기

## 1. Create User

처음 설치할 때 만든 root 계정 이외에 다른 유저를 추가해보자. 

workbench를 통해 유저를 추가하려면 연결이 된 DB에 접속해 Administration 탭에 들어가 MANAGEMENT 중 Users and Privileges를 클릭해 유저를 추가하면 된다. 그러나 workbench 8.0 상에서 비밀 번호 설정에 관련 에러가 발생하기 때문에 Mysql 콘솔창을 이용하자.

#### 1) Database creation

먼저 DB를 생성한다. DB가 이미 있다면 생성할 필요는 없다.

```mysql
mysql> CREATE DATABASE `mydb`;
```

#### 2) User creation

비밀번호를 설정해 유저를 생성한다.

```mysql
mysql> CREATE USER 'myuser' IDENTIFIED BY 'mypassword';
```

#### 3) Grant permissions to access and use the server

유저에게 로컬 호스트상 모든 DB에 접근이 가능하도록 만든다.

```mysql
mysql> GRANT USAGE ON *.* TO 'myuser'@localhost IDENTIFIED BY 'mypassword';
```

localhost뿐 아니라 다른 서버에도 접속이 가능하게 만들 수도 있다.

```mysql
mysql> GRANT USAGE ON *.* TO 'myuser'@'%' IDENTIFIED BY 'mypassword';
```

#### 4) Grant all privilegse to a user

생성한 유저에게 특정 DB에 대한 모든 권한을 부여할 수 있다.

```mysql
mysql> GRANT ALL privileges ON `mydb`.* TO 'myuser'@localhost;
```

localhost를 위처럼 %로 바꾸면 모든 서버가 가능하다.

변경된 사항을 적용시키려면 아래 명령어를 입력해야 한다.

```mysql
mysql> FLUSH PRIVILEGES;
```

#### 5) Check permissions

유저에 해당하는 권한들을 조회할 수 있다.

```mysql
mysql> SHOW GRANTS FOR 'myuser'@localhost; 
```

#### 6) Delete User or DB

유저와 DB는 다음의 명령어로 삭제가 가능하다.

```mysql
DROP USER myuser@localhost;
DROP DATABASE mydb;
```



\+ 참고 사이트: [출처](http://www.daniloaz.com/en/how-to-create-a-user-in-mysql-mariadb-and-grant-permissions-on-a-specific-database/)



## 2. Schema 생성

DB 스키마를 생성하자.

```mysql
CREATE SCHEMA `mydb` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
```

문자 인코딩은 utf8mb4를 지정했다. utf-8은 최대 3바이트로 저장이 되는데, 이모지나 여타 4바이트가 요구되는 문자열이 들어오면 에러가 발생한다. 이를 방지하고자 4바이트인 utf8mb4로 설정을 했다. (utf8mb4는 MariaDB에만 있다. mySQL에서는 utf-8로도 이모지 저장이 가능하다.)

엑세스가 거부되면 권한이 없다는 뜻이므로, 생성한 유저에게 아래 명령어를 통해 권한을 부여하자.

```mysql
GRANT ALL privileges ON `mydb`.* TO `user`@localhost;
```



## 3. Table 생성

이번에 넣을 데이터는 2종류다.

하나는 개선된 도로명 코드 중 2월 분이고, 하나는 보건복지부 선별진료소 데이터 3월 13일 분이다.

<font size=2>- [도로명](http://www.juso.go.kr/addrlink/addressBuildDevNew.do?menu=match)</font>

<font size=2>- [선별진료소](https://www.data.go.kr/dataset/15043008/fileData.do)</font>

도로명 테이블의 이름은 addr이고 칼럼은 `도로명코드,도로명,읍면동일련번호,시도명,입력자 ssafy 아이디,입력일자(년월일시분초)`이다.

선별진료소 테이블 이름은 medical이고 칼럼은 `연번,시도,시군구,의료기관명,주소,대표
전화번호,입력자 ssafy 아이디,입력일자(년월일시분초)`이다.

먼저 CSV 파일로 받은 선별 진료소 데이터부터 처리해보도록 하겠다.

## 4. CSV into Database

받은 자료의 칼럼은 다음과 같다.

`연번,검체채취 가능여부,시도,시군구,의료기관명, 주소,대표 전화번호`

받은 자료의 컬럼이 테이블과 다르더라도, 우선 테이블을 먼저 생성한다.

```mysql
CREATE TABLE `mydb`.`medical` (
  `연번` INT NOT NULL AUTO_INCREMENT,
  `시도` VARCHAR(45) NULL,
  `시군구` VARCHAR(45) NULL,
  `의료기관명` VARCHAR(200) NULL,
  `주소` VARCHAR(200) NULL,
  `대표 전화번호` VARCHAR(45) NULL,
  `SSAFY_ID` VARCHAR(45) NULL,
  `입력일자` DATETIME NULL,
  PRIMARY KEY (`연번`));
```

먼저 최종 테이블을 완성한 뒤, 데이터를 넣으려 했으나 file을 import 할 때 칼럼을 매칭시키는 문제가 발생하였다. 그래서 먼저 데이터를 넣은 뒤 칼럼을 수정하는 방식으로 바꿨다.

---

먼저 넣자.

넣을 데이터와 같은 모양으로 칼럼을 생성한다.

```mysql
CREATE TABLE `mydb`.`medical` (
  `연번` INT NOT NULL AUTO_INCREMENT,
  `가능여부` VARCHAR(5) NULL,
  `시도` VARCHAR(45) NULL,
  `시군구` VARCHAR(45) NULL,
  `의료기관명` VARCHAR(200) NULL,
  `주소` VARCHAR(200) NULL,
  `대표 전화번호` VARCHAR(45) NULL,
  PRIMARY KEY (`연번`));
```

데이터를 추가한다.

```mysql
LOAD DATA 
INFILE 'c:/%PATH%/medical.csv' 
INTO TABLE mydb.medical 
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"' 
LINES TERMINATED BY '\n' 
IGNORE 1 ROWS;
```

그러나 이도 동작하지 않는다. mariaDB는 root 위치에서부터 파일에 접급하는 것을 막아놨다. 그래서 직접 넣을 파일의 위치를 mariaDB가 있는 곳으로 옮겨야 한다.

옮길 위치는 INFILE에 임의의 값을 넣고 코드를 실행하면 에러 메시지로서 확인이 가능하다.

실행결과 다음의 에러 메시지가 출력되었다.

```
Error Code: 29. File 'C:\Program Files\MariaDB 10.4\data\mydb\medical.csv' not found (Errcode: 2 "No such file or directory")
```

이 에러 메시지에서 뜬 것처럼 해당 경로에 원하는 파일을 넣고 아래와 같이 코드를 변경한다.

```mysql
LOAD DATA 
INFILE 'medical.csv' 
INTO TABLE mydb.medical 
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"' 
LINES TERMINATED BY '\n' 
IGNORE 1 ROWS;
```

하지만 이 역시도 실행되지 않는다. 이유는 모든 필드의 구분을 comma로 하였는데 데이터 중 하나의 필드에 두 개의 데이터가 comma로 구분되어있는 행이 있기 때문이다.

가령 다음의 데이터는 문제 없이 들어갈 수 있다.

````
1,Y,서울,강남구,강남구보건소,서울특별시 강남구 선릉로 668 (삼성동),02-3423-5555
````

콤마가 6개로 7개의 칼럼을 지칭한다.

그러나 다음 데이터는 문제가 발생한다.

```
8,Y,서울,강북구,강북구보건소,"서울특별시 강북구 한천로 897 (번동, 강북보건소,번2동주민센터)","02-901-7706,02-901-7704"
```

콤마가 9개로 10개의 칼럼을 의미하는 것처럼 DB에게는 읽힌다. 하지만 이 역시 7개의 칼럼을 의미하며 double quotations marks 안에 있는 comma는 `FIELDS TERMINATED BY ','` 로 해석되어서는 안 된다. 그러나 현재 SQL 문으로는 이를 수정하기가 어려워 보인다. 그러므로 데이터를 전처리 후에 넣어야 한다.

### Data preprocessing

파이썬을 활용해 칼럼의 경계를 `|` 로 바꾸자.

```python
ALL_LINES = []

with open("medical.csv", "r", encoding='utf-8-sig') as file:
    for one_line in file.readlines():
        list_line = list(one_line.replace(',', '|'))
        quot_mark = False
        for idx, val in enumerate(list_line):
            if val == '|':
                if quot_mark:
                    list_line[idx] = ','
            elif val == '"':
                if not quot_mark:
                    quot_mark = True
                else:
                    quot_mark = False
        str_line = ''.join(list_line)
        ALL_LINES.append(str_line)

str_LINES = ''.join(ALL_LINES)

with open("medical_processed.csv", "w", encoding='utf-8-sig') as file:
    file.writelines(str_LINES)
```

이제 최종 결과물을 DB에 넣자

```mysql
LOAD DATA
INFILE 'medical_processed.csv' 
INTO TABLE mydb.medical  
FIELDS TERMINATED BY '|' 
LINES TERMINATED BY '\n' 
IGNORE 1 ROWS;
```

이제 값이 들어간 것을 확인할 수 있다.



### Column 수정

이제 더이상 `가능여부` 칼럼은 필요 없으니 삭제하고, ssafy 아이디 칼럼과 입력일자 칼럼을 추가해야 한다.

삭제는 다음과 같다.

```mysql
ALTER TABLE mydb.medical DROP COLUMN `가능여부`;
```

이제 두 칼럼을 추가하자.

```mysql
ALTER TABLE mydb.medical 
ADD COLUMN SSAFY_ID VARCHAR(200) DEFAULT 'mpcato@naver.com',
ADD COLUMN `입력일자` DATETIME DEFAULT NOW();
```



## 5. Text into Database

이번에는 도로명 주소에 대한 정보가 담긴 txt 파일을 DB에 넣는다.

<font size=3>[도로명](http://www.juso.go.kr/addrlink/addressBuildDevNew.do?menu=match)</font> 링크에서 파일을 다운 받고 전처리를 해야한다.

우리가 원하는 칼럼의 형식은 다음과 같다.

`도로명코드,도로명,읍면동일련번호,시도명,입력자 ssafy 아이디,입력일자(년월일시분초)`

하지만 실제 데이터는 이와 다르다.

```
111102005001|세종대로|Sejong-daero|00|서울특별시|Seoul|종로구|Jongno-gu|||2||0||||
```

고로 이를 우리가 원하는 방식대로 만들어야 한다.

다음과 같이 만든다.

```
111102005001|세종대로|00|서울특별시 종로구
```

변환 코드는 다음과 같다.

```python
ALL_LINES = []

with open("roads.txt", "r", encoding='utf-8-sig') as file:
    for idx, line in enumerate(file.readlines()):
        line = line.split('|')
        result = '|'.join([line[0], line[1], line[3], '{} {}'.format(line[4], line[6])])
        ALL_LINES.append(result)

str_LINES = '\n'.join(ALL_LINES)

with open("roads_processed.csv", "w", encoding='utf-8-sig') as file:
    file.writelines(str_LINES)
```

이에 해당하는 테이블을 만들자.  `PK,도로명코드,도로명,읍면동일련번호,시도명`을 가진 테이블을 만든다. PK는 없어서 추가했다.

```mysql
CREATE TABLE `mydb`.`addr` (
  `PK` INT NOT NULL AUTO_INCREMENT,
  `도로명코드` VARCHAR(200) NULL,
  `도로명` VARCHAR(200) NULL,
  `읍면동일련번호` VARCHAR(200) NULL,
  `시도명` VARCHAR(200) NULL,
  PRIMARY KEY (`PK`));
```

만든 파일의 위치를 옮겨 Load data 를 실행한다.

```mysql
LOAD DATA
INFILE 'roads_processed.csv' 
INTO TABLE mydb.addr 
FIELDS TERMINATED BY '|' 
LINES TERMINATED BY '\n'
(`도로명코드`, `도로명`, `읍면동일련번호`, `시도명`)
SET `PK` = null;
```

이제 칼럼을 추가하자.

```mysql
ALTER TABLE mydb.addr 
ADD COLUMN SSAFY_ID VARCHAR(200) DEFAULT 'mpcato@naver.com',
ADD COLUMN `입력일자` DATETIME DEFAULT NOW();
```

