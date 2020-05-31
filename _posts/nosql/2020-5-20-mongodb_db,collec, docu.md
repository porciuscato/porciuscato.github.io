---
comments: true
title: NoSQL Mongo DB에서 Database, Collection, Document 생성 및 제거
published: false
updated: 2020-5-20
tags: [nosql, mongodb]
categories: [development]
---

NoSQL Mongo DB에서 Database, Collection, Document 생성 및 제거



## Database/Collection/Document 생성 및 제거

#### Database 생성: use

`use DB_NAME` 명령어로 DB를 생성한다. DB가 이미 있는 경우, 있는 DB를 사용한다.

- tutorial이라는 DB를 생성한다.

  ```
  > use tutorial
  ```

- 현재 사용중인 DB를 확인하기 위해 `db` 명령어를 입력한다.

  ```
  > db
  ```

- DB 리스트들을 확인하려면 `show dbs` 를 입력한다.

  ```
  > show dbs
  ```

  그런데 방금 만든 tutorial이 보이지 않는다. 보려면 최소 한 개의 Document를 추가해야 한다.

  ```
  > db.book.insert
  ```

  









#### 참고

- [벨로퍼트](https://velopert.com/457)

