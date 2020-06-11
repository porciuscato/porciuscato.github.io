---
comments: true
title: javascript
published: false
updated: 2020-6-11
tags: [javascript]
categories: [development]
---

자바스크립트의 기본



#### 브라우저 API

brower에 내장된 API

가령

- DOM API
- Geolocation API
- Canvas, WebGL
- Audio and Video APIS(HTMLMediaElement, WebRTC)

\+ Third Party APIS

- Twitter API
- Google Maps API, OpenStreetMap API

등등이 있다. 이런 것들로 엄청난 것들을 만들어 낼 수 있다!!



### 자바스크립트는 페이지에서 어떻게 동작하는가?

브라우저는 서버에서 받은 HTML 파일(HTML, CSS, Javascript)을 DOM 객체로 만든다.



#### 브라우저 보안

보안 상, 브라우저 탭들은 각기 독립 실행 환경이다. 한 탭의 코드가 다른 탭에 영향을 끼칠 수 없도록 만들어져 있다.

> \+ 불가능하지는 않다. 다만 advanced 영역이다.

#### 자바스크립트 실행 순서

위에서 아래로 실행된다.

#### interpreted code vs compiled code

인터프리터는 코드를 순차적으로 실행하며 결과를 즉각적으로 반환한다. 다른 코드로 변경할 필요가 없다. 하지만 컴파일러는 실행하기 전에 어셈블리어로 바꾼 뒤 실행된다. 

자바스크립트는 lightweight interpreted programming language다. 브라우저는 받은 스크립트 코드를 순차적으로 실행한다. 엄밀히 말하면, 기술적으로 JS는 성능향상을 위해  `just-in-time compiling`(JIT)을 한다. 하지만 JS는 컴파일이 실행 시간 전이 아닌 실행 시간에 시행되기에  인터프리터 언어로 여겨진다. 

#### server-side vs client-side code

JS의 클라이언트 사이드적 특성에 대해 주로 이야기할 것이다. JS도 서버 사이드가 가능은 하다.

#### Dynamic vs Static code





출처: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript

- [mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- [learn javascript online](https://learnjavascript.online/)