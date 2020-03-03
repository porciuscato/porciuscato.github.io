---
comments: true
title: javascript의 연산자와 제어구조
published: 2020-3-1
updated: 2020-3-1
tags: [javascript, wrapper, array, json]
categories: [development]

---

Javascript의 범주 중 연산자에 대해 알아보자. 



## 자바스크립트의 범주

`데이터`, `연산자`, `제어구조`, `함수`, `Document Objects`, `Browser Object`



## 연산자

- 산술연산자: +, -, *, /, %
- 비교연산자: <, >, <=, >=, ==, !=, ===, !==
- 관계연산자: &&, ||

다른 언어와 같지만 JS만이 가진 특이한 연산자인 `===`. 이것의 정체는 무엇인가?

비유적으로 표현하자면, JS는 변수를 만들 때 Wrapper, 즉 변수를 감싸는 일종의 박스를 만든다. 다음의 예를 생각해보자.

```javascript
var a = 3
var b = new Number(3)
```

이 둘을 비교해보자

```javascript
console.log(a == b)  // true
console.log(a === b) // false
```

왜 이런 결과가 나오는가?

### `==` & `===`

`==`은 **값**을 비교하는 연산자고, `===`은 **주소**를 비교하기 때문이다.

하지만 주의할 점이 있다. 만약 둘 다 새로운 객체를 만들어서 비교를 한다면 어떻게 될까?

```javascript
var a = new Number(3)
var b = new Number(3)
console.log(a == b)  // false
console.log(a === b) // false
```

분명히 값이 같다고 생각했는데 `==` 에서 false가 나온다. 어떤 게 된 걸까? 이건 나중에...



## 제어구조

- 조건문: if, while, do-while
- 반복문 while, for, for-in
- 선택문 else, else if, switch

다른 언어와 비슷하니 JS만의 특징인 for-in만을 살펴보자

파이썬에서 for in에 리스트를 넘기면 리스트의 값들이 나왔다.

```python
words = ['a', 'b', 'c', 'd']
for word in words:
    print(word)
# a, b, c, d가 출력된다.
```

하지만 JS의 for-in은 이와 다르다.

```javascript
var words = ['a', 'b', 'c', 'd']
for(word in words){
    console.log(word)
}
// 0, 1, 2, 3이 출력된다.
```

그저 index를 넘길 뿐이다. `for(var word = 0; i < words.length; i++)` 이 축약됐다. Object는 key를 넘긴다. 값들을 출력하기 위해서는 다음처럼 코드를 작성하면 된다.

```javascript
// Array
var words = ['a', 'b', 'c', 'd']
for(i in words){
    console.log(words[i])
}

// Object
var ob = {"id": 1, "title": 12, "value": 15}
for(var i in ob){
	console.log(ob[i])
}
```







\+ `console.log()` : 개발자도구 출력, `alert()` : 대화상자 출력, `document.write()` : 문서 출력





#### 참고

- [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)