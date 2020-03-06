---
comments: true
title: javascript의 브라우저오브젝트, Browser Object
published: false
updated: 2020-3-5
tags: [javascript]
categories: [development]
---

Javascript를 통해 브라우저 객체를 다뤄보자



## 자바스크립트의 범주

`데이터`, `연산자`, `제어구조`, `함수`, `Document Objects`, `Browser Object`



## 브라우저 객체

- window : 브라우저 
  - window.location : URL 입력창
  - window.history : 뒤로가기
  - window.document : 화면의 내용. DOM 트리 구조



### 최상위 객체인 window 객체

윈도우 객체에는 여러 하위 객체들이 있다.

- window
  - screen
  - location
  - history
  - document
  - navigator

\+ 윈도우는 생략 가능하다.



\+ 사용가능한 Method와 Properties

#### Methods

- `alert(str)` : 경고창. 브라우저마다 다름
- `confirm(str)` : true or false를 return
- `prompt(str, defaultValue)` : 사용자로부터 입력을 받는 함수 -> 문자열을 받는다.
- `setTimeout()`
- `clearTimeout()`
- `setInterval()`
- `clearInterval()`

\+ alert 등은 자바스크립트 함수가 아니다. 그러므로 모질라 사이트에서 관련 내용을 보기 위해선 Javascript 항목이 아닌 APIs/DOM 이다.

#### Properties

- status
- defaultStatus



\+ 유용한 내장 함수

- `parseInt(string, radix)` : number로 형변환. base에는 진법이 들어감

  - x에 숫자가 아닐 경우 `NaN`을 return 함. (Not a Number)

    \** parseInt('123abc') 의 경우, 123을 return 한다.



### 이벤트 기반의 프로그래밍

script 태그 뿐 아니라 input 태그에도 스크립트 코드를 쓸 수 있다. (스크립트 코드는 파일이 켜지면 실행된다. 반면 특정 태그에 들어있는 JS 코드는 이벤트가 발생했을 때 실행된다.)

가령 `<input onXXX=""/>` 와 같은 경우 특정 이벤트가 발생했을 때 값에 해당하는 스크립트 코드를 발생시킨다.

```html
<body>
    <input type="button" value="출력" onclick="alert('안내입니다.');"/>
</body>
```

input 태그 뿐 아니라 다른 태그들도 가능하다.

하지만 onXXX의 value로 값을 넣으면 코드의 가독성이 떨어지기 때문에 해당 내용을 태그에 직접 넣지는 말아야 한다. 대신 함수를 script 영역에 정의하고, 태그에 함수호출을 사용한다.

```html
<script>
    function printResult(){
        var x, y
        x = parseInt(prompt('x의 값을 입력하세요', 0))
        y = parseInt(prompt('y의 값을 입력하세요', 0))
        alert('결과는 ' + (x + y).toString() + ' 입니다.')
    }
</script>
<body>
    <p onclick="printResult()">실행</p>
</body>
```

#### 문서 객체의 속성 사용하기

html로 작성된 문서는 load, 즉 메모리 상에 올라가며 트리 구조로 만들어진다. 이때 각각의 노드에 접근할 수 있다. 

위의 p 태그에 id를 부여하고 실행 결과를 바꿀 수 있다.

```html
<body>
	<p onclick="printResult()" id="pPrint">실행</p>
</body>
<script>
    function printResult(){
        var x, y
        x = parseInt(prompt('x의 값을 입력하세요', 0))
        y = parseInt(prompt('y의 값을 입력하세요', 0))
        pPrint.innerText = x + y  // 노드
        pPrint.style="font-size:30px;" // 해당 엘리먼트의 속성
    }
</script>
```

\+ `innerText` 는 태그에 담긴 노드다. `style`은 태그의 속성이다.

`id` 를 사용하여 호출되는 JS 코드를 수정하는 것이 유지보수에 좋으므로 위의 코드를 다음과 같이 바꾼다.

```html
<script>
	function printResult(){...}
    pPrint.onclick = printResult;
</script>
<body>
	<p id="pPrint">실행</p>
</body>
```

> pPrint.onclick = pPrintResult() 라 쓰면 스크립트가 읽히면서 바로 함수가 호출된다. 괄호를 빼서 함수 객체를 전달했다.

그러나 위의 코드는 에러가 발생한다.  pPrint를 모르기 때문이다. 문서를 로드하는 과정에서 script는 선언되지 않은 변수를 참조했다. 그래서 window에 있는 모든 속성들이 로드가 되었을 때 특정 함수를 선언하게 만들 수 있다. 아래와 같이 코드를 바꾸자.

\+ `onload` : 특정 엘리먼트의 하위 엘리먼트들이 모두 메모리에 로드가 되었을 때를 의미한다.

```html
<script>
	function printResult(){...}
    function init(){
	    pPrint.onclick = printResult
    }
	window.onload = init
</script>
<body>
	<p id="pPrint">실행</p>
</body>
```



#### 객체 아이디 명명의 문제

주의할 것은 html은 camelCase를 사용하지 않는다. kebab-case를 사용하는데, kebab을 사용할 경우 JS에서 오류가 난다. 그렇기에 이를 변환하는 과정이 필요하다.

```html
<script>
	function printResult(){...}
    function init(){
        var pPrint = document.getElementById('p-print')
	    pPrint.onclick = printResult
    }
	window.onload = init
</script>
<body>
	<p id="p-print">실행</p>
</body>
```

> 전역 변수는 바람직한 방법이 아니다.

이때 pPrint 변수가 매 함수마다 호출되는 것은 DRY하지 못하다. 그러므로 이를 아래와 같이 바꿔준다.

```html
<script>
    window.onload = function () { // 함수명이 필요없다.
        var pPrint = document.getElementById('p-print')
        pPrint.onclick = function () {
            var x = parseInt(prompt('x의 값을 입력하세요', 0))
            var y = parseInt(prompt('y의 값을 입력하세요', 0))
            pPrint.innerText = x + y
            pPrint.style="font-size:18px;"
        }
    }
</script>
<body>
	<p id="p-print">실행</p>
</body>
```



#### View와 Controller 분리하기

현재 방식은 모든 코드들이 한 페이지에 있기에, 협업의 어려움이 있다. 그러므로 스크립트와 html을 분리하는 방식을 알아보자.

script를 다른 파일에 만든 뒤, head에 script 태그를 추가하자

```html
<script src="index.js"></script>
```

그리고 다른 하나를 추가해보자. test.js를 만들어 아래의 내용을 넣어보자.

```javascript
window.onload = function(){
    this.alert('안녕하세요')
}
```

html의 head는 아래와 같이 고친다.

```html
<script src="index.js"></script>
<script src="test.js"></script>
```

실행을 하면 test.js는 실행이 되는데 index.js는 실행되지 않는다. 어떻게 된 것인가?

이는 `window.onload`가 재할당되었기 때문이다. => `이벤트를 누적`하는 방법을 사용하자!

#### 여러 스크립트 파일을 함께 사용할 때 초기화 함수의 문제

기존에 문제가 되던 표기는 아래와 같다.

```javascript
window.onload = function(){}
```

이를 아래와 같이 바꿔준다.

```javascript
window.addEventListener("load", function() {alert('test1')})
```

이후 코드가 실행된다.

이벤트를 바인딩할 때는 무조건 `addEventListener`를 사용하자.





#### 참고

- [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)