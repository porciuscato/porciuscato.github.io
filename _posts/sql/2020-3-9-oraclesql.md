---
comments: true
title: sql 공부
published: false
updated: 2020-3-8
tags: [sql, oracle]
categories: [development]
---

Oracle SQL을 배워보자



## SQL 이란?

sql은 DBMS에게 질의하는 명령어다.

- DBMS -> 데이터베이스 관리 시스템
- 질의 -> 구조화된 데이터를 질의한다.

### 데이터베이스란 무엇인가

DB는 왜 나왔고 어떤 특징이 있는지 알아보자.

과거에도 컴퓨터는 있었고 데이터들이 있었다. 그러나 네트워크는 연결되지 않은 채 로컬로 데이터들이 관리되는 상황이다. 이때 부처별로 데이터 공유가 되지 않기 때문에 싱크의 문제가 발생한다. 싱크의 시간 격차로 인해 데이터 결함도 발생하게 된다.

이를 효과적으로 관리하며 데이터 결함도 없애기 위한 방법으로, 한 곳에 모아놓는 방법을 고안한 것이 DBMS다. 

그러나 단점도 있다. 데이터의 중복을 없애는 과정에서 테이블이 분할되었고, 이들을 붙이기 위한 참조 작업이 필요하다. 참조없이는 그 데이터들의 의미를 파악하기가 어렵다.

그래서 참조 모델을 고안하는 여러 방법들이 제안되었다.

Hierachical DBMS, Network DBMS, Object-Oriented DBMS, Relational DBMS 등 여러 방법들이 제안되었다. 

결국 현재 우리가 사용하는 모든 데이터베이스들은 관계형으로 구현되었다.

또 다른 문제가 있다. 같은 데이터를 서로 동시에 수정하는, `병목 현상`이 발생할 수 있다.

또 여럿이 사용하다보니 `성능`에 문제가 발생했다.

또 여럿이 같이쓰다보니 `보안` 문제도 발생한다.

이러한 문제를  해결해주는 *관리자*를 통해서 사용하는 것이다. -> 프로그램이 직접 파일에 접근하지 않는다. 데이터베이스는 관리자를 통해서만 접근해야 한다.

관건은 이 관리 시스템을 만드는 것이다. 현존하는 기업들 중 관리 시스템을 가장 잘 만드는 회사는 Microsoft SQL Server, MySQL, ORACLE 등이 있는데 우리는 ORACLE을 통해 공부를 해보자.



### SQL(Structured Query Language)

앞으로는 데이터에 직접 접촉하지 않는다. 다만 관리자를 통해 접근한다. 이런 부탁을 할 때 사용하는 것이 query language다. 그런데 structured인 이유는 쿼리를 통해 받는 데이터가 단순히 int, char 값이 아닌 구조화된 데이터, 더 큰 단위의 데이터 묶음이기  때문이다. 



## ORACLE DBMS 설치

[오라클](https://www.oracle.com/database/technologies/oracle-database-software-downloads.html) 사이트로 들어가서 하단의 Oracle Database Express Edition 중 Oracle Database 18c Express Edition을 다운 받자.

압축을 푼 뒤 관리자 권한으로 설치를 진행해야 한다. 파일로 들어가 `setup.exe` 파일을 관리자 권한으로 설치하자.

설치가 끝나면 https://localhost:5500/em 에 접속해 웹으로 DB 관리가 가능하다. 보안 관련 경고가 뜨는데 무시하고 넘어가면 된다. 이때 아이디는 sys고, 비밀번호는 설치할 때 입력했던 것을 적으면 된다. 하지만 이걸 쓰지는 않을 예정이다.



## DB 서버에 접속하기

오라클 자체는 서버 프로그램이다. 이에 요청을 보낼 클라이언트 프로그램 역시 필요하다. 오라클이 제공하는 클라이언트는 콘솔 기반의 SQL plus와 윈도우 기반의 SQL developer다. 사용자는 이 프로그램으로 서버와 통신이 가능하다. 

설치된 프로그램 중 sql plus를 찾고 사용자명에 `sys as sysdba`를 입력하면 서버에 접속이 가능하다.

> 혹은 cmd 창에서 
>
> ```
> sqlplus sys as sysdba
> ```
>
> 를 입력해도 접속이 가능하다.

GUI를 제공하는 sql develop도 사용해보자. 오라클 다운로드 [페이지](https://www.oracle.com/downloads/)로 들어가, SQL developer를 다운받는다. 압축 파일을 해제 후 설치 폴더에 들어가 sqldeveloper.exe를 실행한다.

왼쪽 초록색 + 버튼을 클릭해, 데이터 베이스를 새로 만든다. 



## 오라클 PDB 서버에 접속하기

=> Pluggable DataBase

가상화된 데이터 베이스를 의미한다. 가상화된 프로그램을 다른 곳에 이식이 가능하듯, 이 DB도 탈부착이 가능하다.

위에서 sql developer를 통해 접속한 DB는 과거의 CD, 즉 Container DB에 접근한 것이다. 여기에 PDB를 만든다는 것은 가상 데이터 베이스를 만드는 것이다.

### 접속해보기

먼저 sqlplus를 실행해서 다음의 명령어를 통해 pdb를 확인해보자.

```
select name from v$pdbs;
```

그러면 결과로서 

```
PDB$SEED
XEPDB1
```

이들을 확인할 수 있다. Seed는 원본의 의미를 가지고 실제 만들어진 pdb는 XEPDB1이다. 이것이 하나의 가상 데이터베이스다. CDB는 손상이 가해지면 부담이 크지만, PDB는 망가져도 큰 문제가 안 생기기 때문에 앞으로 이를 통해 연습을 할 것이다.

그러면 XEPDB1에 접속해보자.

sql developer에 들어가서 왼쪽 사이드바에서 접속 밑의 초록색 + 버튼을 누르고 새로운 접속 유형을 만든다. 이때 주의할 점은 세부정보에 SID가 선택되어있는데, 이를 서비스 이름으로 바꾼 뒤 `xepdb1`을 입력한다.

> \+ DB를 원격에서 접속하기 위해선 설정을 바꿔야 한다. 아래의 명령어를 통해 설정을 바꿀 수 있다.
>
> ```
> EXEC DBMS_XDB.SETLISTENERLOCALACCESS(FALSE);
> ```
>
> 로컬로만의 접속을 false 한다는 뜻이다. 본래는 로컬 접속만 가능하기에 default로 True다. 위 명령어를 sql plus에 입력하자.
>
> 이후 다른 컴퓨터에서 접속이 가능하게 하려면 sql developer에서 설정을 바꿔야 한다. 초록색 + 버튼을 클릭하고 세부정보에 들어가 호스트이름으로서 localhost로 되있는 것을 IP 주소로 바꾼다. (이는 cmd 창에서 ipconfig를 입력해 확인할 수 있다.)





#### 참고

- [newLecture](https://www.youtube.com/watch?v=pGlkIFrY9QY&list=PLq8wAnVUcTFVq7RD1kuUwkdWabxvDGzfu)

