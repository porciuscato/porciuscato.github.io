---
comments: true
title: javascript의 클로저
published: false
updated: 2020-3-2
tags: [javascript]
categories: [development]
---

Javascript의 클로저에 대해 알아보자.



## 클로저

JS는 함수를 정의하지 않고 함수를 객체로 만든다. 함수를 객체로 만들기 때문에 그 객체가 반환될 수 있고, 함수가 객체 안에서 만들어질 수도 있다. 이떄 함수가 만드는 지역변수가 클로저의 문제를 일으킨다.

? 잘 이해 안 됨

뉴렉 17강. 함수를 내포한 함수에서 상위 함수가 지역 변수로 사용한 것이 하위 함수에서도 호출 된다면 상위 함수의 생명 주기가 다했음에도 변수를 해제하지 못하는 현상. 이때 하위 함수까지 호출이 끝나야 상위 함수의 지역변수는 해제될 수 있다. 이때 하위 함수가 상위 함수의 지역 변수를 종료시켜주는 키의 역할을 하기 때문에 이를 클로저(closure)라 부른다.





- [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)