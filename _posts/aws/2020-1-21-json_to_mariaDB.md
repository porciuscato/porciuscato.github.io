---
title: windows에서 JSON 파일을 mariaDB에 넣기
published: false
updated: 2020-1-21
tags: [mariaDB, json, windows]
categories: [development]
---

json으로 만든 seed data를 mariaDB에 넣어봅시다.



  API를 통해 가져온 정보는 JSON, XML 파일의 형식입니다. 이를 그대로 DB에 넣을 수 있다면 얼마나 좋을까요! 이번엔 이 방법에 대해 알아보도록 하겠습니다.

  순서는 다음과 같습니다.

- MariaDB를 설치합니다.
- 이후 MariaDB connect-engine을 설치합니다.

work bench 설치



### 1. MariaDB 설치

  이번에 사용할 DB는 Maria DB입니다. 오라클 소유의 MySQL에 반발해 오픈소스로 만들어진 DB입니다. Maria DB는 MySQL의 소스코드를 기반으로 만들어진 DB이며 MySQL의 문법을 지원하기에 그것과의 호환성도 높습니다. 

  설치를 위해 다운로드 [링크](https://downloads.mariadb.org/)로 들어갑니다.

  글을 작성하는 시점에서는 안정된 버전인 10.4 를 다운 받았습니다. 

- 64bit용 윈도우즈 설치파일을 다운 받습니다. `mariadb-10.4.11-winx64.msi` 입니다.
- 파일이 다운받아졌으면 설치 파일을 실행합니다.

- Next를 누르며 설치를 진행합니다.
- Default instanace properties
  - root password를 설정합니다.
  - 이때 원격 머신에서 DB에 접근 가능하게 하려면 `Enable access from remote machines for 'root' user`에 체크합니다. 로컬에서만 사용하려면 체크할 필요 없습니다.
  - `Use UTF8` 를 선택합니다.
  - 서비스 네임, networking 등도 기본값으로 진행합니다.
  - 이후 설치를 진행합니다.
- 설치가 완료되면 윈도우즈 시작버튼에서 MariaDB 10.4 프로그램 그룹을 찾고
  - MySQL Client를 실행합니다.
- root 비밀번호를 입력하고 `show databases;`를 입력해서 설치된 DB를 확인해 봅니다.

여기까지 진행되었으면 설치가 잘 된 것입니다!



### 2. connect-engine 설치

  MySQL Client를 실행하여 `show engines;` 를 입력하여 현재 설치된 엔진들을 확인합니다. 

  없으면 설치해줍시다.



??

choco install mariadb





### 2. JSON 파일을 테이블에 적재하기



```
AWS maria DB 접속하기
15.165.77.1:3306
id : ssafy
pw : ssafy
```

-> workbench로 들어가기







DB에 query를 작성해서 일일이 데이터를 넣는 것은 번거로운 일입니다. 



참고

[[Admin][MariaDB] JSON 테이블에 적재(Json Table Type)](https://estenpark.tistory.com/350)





1. mariaDB를 설치하자