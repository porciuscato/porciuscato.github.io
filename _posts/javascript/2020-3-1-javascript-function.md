---
comments: true
title: javascript의 함수와 표현식
published: false
updated: 2020-3-1
tags: [javascript]
categories: [development]
---

Javascript의 범주 중 함수에 대해 알아보자. 



## 자바스크립트의 범주

`데이터`, `연산자`, `제어구조`, `함수`, `Document Objects`, `Browser Object`



## 함수

JS는 함수를 '정의'하지 않는다. 그런데 함수는 있다. JS에서는 함수를 '만든다'.

```C++
int add(int x, int y) return x + y;
```

이런 식으로 정의하지 않고

```javascript
new Function("x, y", "return x + y")
```

함수 객체를 만든다. 그리고 객체에는 이름이 필요하기에 add라는 이름을 붙인다.

```javascript
var add = new Function("x, y", "return x + y")
```

Function 객체는 두 개의 문자열을 받는데, 앞에는 인자, 뒤에는 구현 로직이다.

다른 언어처럼 함수를 만들 수 있다. 다만 함수 객체를 만든다는 점에서는 위와 같다.

```javascript
var add = function(x, y){
    return x + y
}  // => 이 방법을 가장 많이 씀
// 혹은
function add(x, y){
    return x + y
}
```

\+ 함수도 객체이기에 다른 함수에 인자로서 넘길 수 있다.





#### 참고

- [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)