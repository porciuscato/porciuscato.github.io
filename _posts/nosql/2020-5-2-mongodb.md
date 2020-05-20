---
comments: true
title: NoSQL Mongo DB에 대해 알아보자
published: false
updated: 2020-5-2
tags: [nosql, mongodb]
categories: [development]
---

NoSQL인 MongoDB에 대해 알아보자.



## MongoDB 소개

- MongoDB란?

  - C++로 작성된 오픈소스 문서지향(Document-Oriented)적 Cross-platform 데이터베이스다.
  - 뛰어난 확장성과 성능을 자랑
  - 현존하는 NoSQL DB 중 인지도 1위

- NoSQL이란?

  - Document-oriented 데이터베이스

    - Document는 한 개 이상의 key-value pair로 이루어진 자료구조

    - example

      ```json
      {
          "_id": ObjectId("5099803df3f4948bd2f98391"),
          "username": "velopert",
          "name": { first: "M.J.", last: "Kim" }
      }
      ```

      - _id는 hexadecimal 값으로 각 document에 유일함(uniqueness)을 제공한다.
        - 첫 4 bytes는 현재 timestamp, 다음 3 bytes는 machine id, 다음 2 bytes는 MongoDB의 프로세스 id, 마지막 3 bytes는 순차번호

    - Document는 동적 schema를 가지고 있어, 같은 Collection 안에 있는 Document일 지라도 다른 schema, 즉 다른 데이터 key 들을 가질 수 있다.

  - Collection

    - MongoDB의 Document 그룹이다. Document들은 Collection 내부에 위치해 있다.
  
  - 장점
    - Schema-less : Schema가 없다. 같은 Collection일지라도 다른 Schema를 가질 수 있다.
    - 각 객체의 구조가 뚜렷하다.
    - 복잡한 JOIN이 없다.
    - Deep Query ability : 문서지향적 Query Language를 사용하여 SQL만큼 강력한 Query 성능을 제공한다.
    - 어플리케이션에서 사용되는 객체를 데이터베이스에 추가할 때 Conversion / Mapping이 불필요하다.



## MongoDB 설치

[다운로드 페이지](https://www.mongodb.com/download-center/community) 로 가, 운영체제에 맞는 DB를 설치한다.

기본 데이터 위치는 
`C:\Program Files\MongoDB\Server\4.2\data\`이고, 로그 위치는 `C:\Program Files\MongoDB\Server\4.2\log\`이다.



## Mongo DB 모델링

- RDBMS와 비교를 위해 간단히 블로그 DB 모델링에 대해 생각해보자. 글과 태그, 커맨트를 연결하려면 테이블을 3개를 만들어야 한다. 그러나 NoSQL에서는 아래와 같이 하나의 Document에 넣는다.

  ```json
  {
      "_id":"POST_ID",
      "title":"POST_TITLE",
      "content":"POST_CONTENT",
      "username":"POST_WRITER",
      "time":"POST_TIME",
      "tags":[TAG1, TAG2, TAG3],
      "comments":[
          {
              "username":"COMMENT_WRITER",
              "mesage":"COMMENT_MESSAGE",
              "time":"COMMENT_TIME"
          },
          {
              "username":"COMMENT_WRITER",
              "mesage":"COMMENT_MESSAGE",
              "time":"COMMENT_TIME"
          }
      ]
  }
  ```



#### 참고

- [벨로퍼트](https://velopert.com/436)

