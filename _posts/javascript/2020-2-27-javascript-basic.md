---
comments: true
title: javascript의 데이터 객체와 래퍼 클래스, Array, Object, JSON
published: 2020-2-27
updated: 2020-2-27
tags: [javascript, wrapper, array, json]
categories: [development]
---

Javascript의 범주 중 데이터에 대해 알아보자. 데이터 범주 중 데이터 객체와 래퍼 클래스, Array, Object, JSON에 대해 알아보자



## 자바스크립트의 범주

`데이터`, `연산자`, `제어구조`, `함수`, `Document Objects`, `Browser Object`



## 데이터

언어들의 기본 데이터 형식은 아래와 같은 것들이 있다. 

- 정수
- 실수
- 문자
- 문자열

그런데 일반적인 언어와 달리 이 모두를 JS는 `var` 키워드로서 변수를 선언한다. int, float 등을 사용하지 않는다.

```javascript
var x = 3;
var x = 3.7;
var x = 'A';
var x = "Hello";
```

어떻게 `var` 키워드만으로 가능한가? 변수는 값을 담는 공간을 의미하는데, 변수를 위한 공간을 어디에 할당하는 것인가?

=> 자바스크립트는 공간을 만들지 않는다! `var` 는 모두 참조변수다. rvalue는 lvalue에 담겨지는 것이 아니라, 스스로가 공간을 갖게 된다. -> 이를 `auto boxing`이라 한다. 혹은 `auto wrapping` 이라 한다.

- 변수는 포인터가 아니라 `참조`다. 포인터는 주소를 저장하는 변수고 변수기에 자체적인 공간을 가지고 있다. 반면 참조 변수는 포인터와 달리 주소를 가지지 않고 이름에 불과하다. 변수가 아니다. 
- 이런 변수는 객체지향이기에 필요한 개념이다. 
  - ex) 개를 한 마리 키운다고 가정해보자. 개를 '개'라고 부르는 것은 하나의 객체를 지칭하는 것이 아닌 '개'라는 생물종의 개체를 지칭하는 것과 같다. 
  - 객체에 이름을 부여하듯, 이 객체를 참조할 변수가 필요하다. 
  - 물론 내부적으로 참조 변수도 주소를 가지고 있겠지만, 개념적으로는 객체에 대한  `이름` 이다.
- 자바스크립트는 모든 데이터가 박싱이 된다. 그리고 모든 데이터를 참조하는 형태로서 모든 변수는 참조변수다.
- 자바스크립트는 문자와 문자열을 구분하지 않는다. 모두 문자열이기에 `''`, `""` 둘 다 같은 의미다.

\* 자바스크립트는 기본형식(int, float 등등)이라는 것이 없다. 다 `wrapper 형 클래스`다.



## Wrapper 클래스와 Wrapping 방식

그러므로 우리가 알아야 하는 것은 Wrapper다. Wrapper 클래스의 종류는 많지 않다.

- 부울: Boolean
- 정수: Number
- 실수: Number
- 문자: String
- 문자열: String

결국 `Boolean`, `Number`, `String` 3가지다.

```javascript
var x = 3;
// 위처럼 선언해도 실제로는 아래와 같은 작업이 일어난다.
var x = new Number(3);
// wrapper 클래스에 의해 박싱이 일어난다.
```

만약 `var x`처럼 변수만 선언한다면 어떻게 될 것인가? `undefined`가 나온다.

- `undefined`는 nullptr와 같다. 

타입을 확인하고 싶으면 `typeof`를 사용하자. 

```javascript
var x = 3
console.log(typeof x)
```


\+  어떤 메소드를 사용할 수 있는지는 할당되는 객체에 따라서 달라진다.



## Array 객체

array 객체는 `Stack` 형식으로 쓸 수 있다. (push, pop을 지원)

```javascript
var nums = new Array() // 이는 var nums = [] 와 같다.
nums.push(1)
nums.push(2)
nums.push(3)
nums.push(4)
nums.pop()
console.log(nums)
// Array(3) [1, 2, 3]
nums.pop()
console.log(nums)
// Array(2) [1, 2]
```

`List` 형식으로도 쓸 수 있다.

```javascript
var nums = new Array()
nums[0] = 5;
nums[1] = 10;
console.log(nums)
console.log(nums[0])
```

- 만약 index를 건너뛴다면?

  ```javascript
  var nums = new Array()
  nums[5] = 20
  console.log(nums)
  // Array(6) […, 20]
  console.log(nums.length)
  // 6
  ```

  => 해당 인덱스를 제외하고 빈 값으로 Array가 채워진다.

  ​	\+ nums[0]으로 접근하면 undefined가 나온다.



### Array 초기화

```javascript
var x = new Array() // Array 형식 선언
var x = new Array(5) // 크기 지정
var x = new Array(1, 2, 3) // 2개 이상일 경우 초기값
var x = new Array(1, 2, 3, "hello") // 다른 데이터 형식도 넣을 수 있음
var x = new Array(1,2,"hi", new Array(3,4)) // Array도 넣을 수 있음
```



## Array 내장함수

- `splice(index, count, value)`

  - destructive / return No
  - index : 몇 번째 위치에서 / count : 몇 개를 지워라 / value : 그리고 그 위치를 value로 바꿔라

  ```javascript
  // 위치 이후 지우기
  var nums = new Array(5, 2, 3, "hello", 20)
  nums.splice(2)
  console.log(nums)
  >>> Array(2) [5, 2] // 2 번째 이후 전부 지워짐
  
  // 몇 개 지우기
  var nums = new Array(5, 2, 3, "hello", 20)
  nums.splice(2, 2)
  console.log(nums)
  >>> Array(3) [5, 2, 20] // 2 번째 이후 2개 지우기
  
  // 지우고 대체하기
  var nums = new Array(5, 2, 3, "hello", 20)
  nums.splice(2, 2, [1, 2, 3])
  console.log(nums)
  >>> Array(4) [5, 2, Array(3), 20]
  ```





## Object 객체

객체 지향언어는 Object를 가지고 있다. 클래스의 형식으로 Object를 정의하고 실체화하여 객체로 만듦. 그러나 자바스크립트는 이와 다름. 기존의 언어는 클래스를 만들고 객체를 만들지만, JS는 객체를 만들고 이후에 정의한다.

JS는 Prototype와 Class가 있지만 이는 후에 정리하도록 하자.

여튼 JS는 Object를 생성한 이후, 필요한 속성을 붙인다.

```javascript
var exam = new Object() // 이는 var exam = {} 와 같다. 파이썬의 딕셔너리와 비슷하다.
exam.kor = 30
exam.eng = 70
exam.math = 80
///
exam["kor"] = 40 // 이런 식으로도 사용할 수 있다.

// 여러 줄을 표현할 경우 ` \`을 사용한다.
var n = '{ \
            "kor": 12, \
            "eng": 30 \
        }'
```

이를 확장이 가능한 Object라 하여 `Expand Object`라 한다.



## JSON

JS는 다른 언어처럼 공간을 할당한 뒤 그 공간에 값을 할당하는 것이 아니다. 객체를 먼저 생성한 뒤 변수는 참조할 뿐이다. JS의 모든 변수는 참조 변수다. 

그래서 정수 하나를 사용하려해도 다음과 같이 객체를 먼저 생성해야 한다. 이는 JS의 다른 데이터 타입도 마찬가지다.

```javascript
// JavaScript Object
var n = new Boolean(true)
var n = new Number(3)
var n = new String("hello")
var n = new Array()
var n = new Objects()
```

매번 변수를 선언할 때마다 객체를 생성해야 한다면 여간 불편한 일이 아닐 수 없다.  그래서 JS가 다루는 오브젝트를 쉽게 표현하기 위해 새로운 표기법이 제시되는데 그것이 `JSON(JavaScript Object Notation)`이다. 

JSON 형식으로 표현하면 위의 코드는 아래처럼 변하게 된다.

```javascript
// JavaScript Object Notation
var n = true
var n = 3
var n = "hello"   // var n = 'hello'와 같다.
var n = []
var n = {}
```

데이터를 전송하는 방식으로서 XML, CSV 등이 있었지만 JSON의 편리함으로 인해 다양한 플랫폼에서도 이를 사용하기 시작했다.

그러나 다른 사이트로서 JSON을 받으면 문자열로 받게 된다. 이를 사용이 가능하도록 Object로 만들어야 한다. 이때 사용 가능한 함수가 `eval()`이다.

### eval

```javascript
'var x = 30'
console.log(x)
// 이는 실행이 되지 않는다. 그런데
eval('var x = 30')
console.log(x)
// 이는 실행이 된다!
```

eval 함수는 string을 실행시키는 역할이다. 그런데 eval 함수 자체는 undefined를 return 하기에 다른 변수가 참조하도록 만들 수는 없다. 그렇다면 문자열로 받은 JSON을 어떻게 바꿔야 하는가?

```javascript
var n = '{ \
            "kor": 12, \
            "eng": 30 \
        }'
eval("var en = " + n)
console.log(en.kor)
// 이렇게 하면 작동한다.
```

하지만 eval 보다는 JSON parser를 이용하는 것이 권장된다. eval 함수는 매번 다른 변수를 추가해줘야하는 번거로움이 있기 때문이다. 그렇기에 JSON Parser를 사용한다.

### JSON Parser

```javascript
var n = JSON.parse('{ \
            "kor": 12, \
            "eng": 30 \
        }')
console.log(n.kor)
// 12가 출력되는 것을 확인할 수 있다.
```

\+ 한 가지 주의하자. 원래 key는 따옴표 안에 넣을 필요가 없다. {kor: 12, eng: 30}으로 해도 동작은 한다. 그러나 parser를 사용할 땐 반드시 Key를 따옴표 안에 넣어야 한다.

허나 key에 큰 따옴표를 붙이지 않는 것이 관례다. Object를 JSON으로 바꾸기 위해 key에 따옴표를 일일이 붙일 필요가 없다. `JSON.stringify` 를 사용하면 된다.

```javascript
var data = {id: 2, title: 'bbb'}
str_data = JSON.stringify(data)
console.log(str_data)
// {"id":2,"title":"bbb"} // 바뀐 것을 확인할 수 있다.
```





#### 참고

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)