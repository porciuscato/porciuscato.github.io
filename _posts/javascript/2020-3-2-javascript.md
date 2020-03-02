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



### 함수의 매개변수, arguments

JS의 매개변수는 여타의 언어와 다르다. 값을 받는 그릇으로서의 역할을 하지 않는다. JS의 모든 변수는 객체이기 때문에 넘겨받는 모든 것들에 대한 참조일 뿐이다.

가령

```javascript
// 함수를 정의하고
function add(x, y){
    return x + y
}
// 아무런 문제가 되지 않는다.
console.log(add(1,2,3,4,5,6,"hello"))
```

대신 받은 모든 매개변수는 `arguments`라는 객체에 담기게 된다.

```javascript
function add(x, y) {
    console.log(arguments.length)
    return arguments[0] + arguments[1]
}
```



### 변수의 영역

변수의 동작을 이해해보자.

- var 선언 변수는 정적인 방식으로 생성

  - 선언된 변수는 어디에서 선언되든 준비된 상태다.

    ```javascript
    console.log(a)
    var a = 1
    ```

    위처럼 코드를 적어도 에러가 나지 않는다. 다만 a는 `undefined` 다.

- global 변수는 동적인 방식으로 생성

  - 변수 앞에 아무것도 쓰지 않으면 그 변수는 전역 변수가 된다. *전역 객체에 속성*을 더하는 것이다.
    - 브라우저의 경우 window이기에 `a = 1`을 선언하면 `window.a`와 같다.

- 지역 변수와 전역 변수의 이름이 같을 경우 지역 변수의 우선순위가 높다.

- JS에서 {}는 변수의 범위를 제한하지 않는다.



\+ JS는 함수 안에 함수 정의가 가능하다.

```javascript
function f1(){
    var a = 1
    f2()
    function f2(){
        var a = 2
        function f3() {
        	var a = 3
        }
    }
}
```





#### 참고

- [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)