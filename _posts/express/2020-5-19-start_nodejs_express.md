---
comments: true
title: express로 API 서버 빠르게 만들어보자
published: false
updated: 2020-5-19
tags: [nosql, node.js, express]
categories: [development]
---

express로 API 서버 빠르게 만들어보자



### Express는?

> node.js 웹 서버 프레임워크다. 



### 서버 만들기

1. 설치

   ```bash
   mkdir myapp
   cd myapp
   npm init
   ​```
   npm install express --save
   ```

   > `--save` 옵션을 통해 설치된 Node 모듈은 package.json 파일 내의 dependencies 목록에추가된다. 이후 app 디렉터리에서 npm install을 실행하면 종속 항목 목록 내의 모듈이 자동으로 설치된다.

2. 서버 코드

   myapp 디렉터리에 `app.js`라는 파일을 만들고 아래의 코드를 작성한다.

   ```javascript
   const express = require("express")	# express 불러오기
   const app = express()								# express 인스턴스 생성
   
   app.get()														# html 요청 방법
   app.post()
   app.put()
   app.delete()
   ```

   - 예시

     ```javascript
     app.listen(3000, () => console.log("Listening on porrt 3000..."))
     
     app.get('/', (req, res) => res.send("Hello World!"))
     ```

     > - app.listen을 통해 포트 번호를 지정할 수 있다.
     >
     > - app.get의 매개변수로 크게 세 가지가 들어간다.
     >
     >   => (url, parameter, next function)
     >
     >   - url은 요청이 들어오는 url의 형식이다.
     >
     >   - parameter로 request와 response를 받는다. 콜백 함수를 연속으로 수행하려면 next를 추가로 넣는다.
     >
     >     ex) (req, res, next)
     >
     >     
     >   





#### 출처

- https://velog.io/@smooth97/Node.js-Restful-API-wok2wqo7yu





