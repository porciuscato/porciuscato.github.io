---
comments: true
title: javascript
published: false
updated: 2020-2-26
tags: [javascript]
categories: [development]
---

Javascript의 기초에 대해 공부한 내용을 적었습니다.



# HTML 객체화

HTML로 작성한 문서는 텍스트에 불과하다.

```html
<body>
  <div>
    등등
  </div>
</body>
```

위 처럼 작성한 코드는 Load가 되면 객체 트리(Document Objects)로 만들어지게 된다. 각각의 태그는 노드가 되어 트리 모양을 형성한다. 이 트리가 사용자 인터페이스로 보여지는 것이다. 각각의 노드는 사용자의 입력 혹은 자바스크립트로 그 내용을 변경할 수 있다.



# 자바스크립트 학습 내용

- 자바스크립트를 사용한 연산, 제어, 저장

- 사용자 입출력으로서 문서 객체를 다루는 방법. 

  - `window` 객체를 통해 브라우저를 통제할 수 있다.

  - `window.location`, `window.history` 등을 사용할 수 있다.

  - `window.document` 를 통해 HTML 문서를 조작할 수 있다.

    등등

```
자바스크립트 -> Document Objects -> Window Object
```



# 자바스크립트의 탄생과 플랫폼

### 자바스크립트의 탄생

90년대 유행했던 브라우저였던 Netscape, 지금은 찾기 어렵다. MS가 브라우저를 무료로 배포하고 이에 대항하여 98년에 MS에 소송을 걸었다. 소송이 길어지며 결국 회사는 문을 닫게 된다. 이 회사가 자바스크립트를 탄생시켰다.

자바스크립트는 서버 자원을 줄이려는 목적으로 만들어졌다. 가령 로그인 페이지를 생각해보자. 로그인 버튼을 누르면 POST 되는 값이 유효하든 하지 않든 서버로 요청이 보내지게 되고, 누군가 이를 과도하게 많이 클릭하면 그 횟수 만큼 서버에 요청이 가게 된다. 이는 곧 서버 자원의 낭비다. 여러 컴퓨터로 진행한다면 DDoS나 마찬가지인 것이다. 

그래서 페이지 자체에서 유효한 값이 들어왔을 경우에만 서버로 요청을 보낼  수 있도록 만들고자 했다. 이를 위해 만들어진 것이 `Form 객체`다. Form 객체는 사용자의 입력을 확인한다. 

HTML 문서가 브라우저에 도착하면 이는 객체 트리로 만들어지고 이 중 form 객체로 사용자의 입력을 받는다. 이때 입력값이 유효하면 서버로 요청을 보내고 그렇지 않으면 보내지 않는다.

자바스크립트는 유효성 검사를 위해 만들어진 언어였다.





> ####  \+ 스크립트 코드 작성 영역
>
> js는 스크립트 태그 안에 넣어야 한다. 이 태그는 html 중 head 혹은 body 어디에 들어가도 무방하다. 태그들이 분산되어 있어도 이를 하나로 인식하기 때문이다.



## 작성한 자바스크립트를 vscode를 통해 웹서버로 열어보자

vscode에서 html 파일을 만들고 간단한 코드를 작성한 다음에 이를 간단하게 웹 서버로 실행시킬 수 있다. 이때 vscode extension인 `Live Server`를 다운받자.



#### 참고

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)