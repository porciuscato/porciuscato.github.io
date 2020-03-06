---
comments: true
title: javascript의 노드
published: false
updated: 2020-3-6
tags: [javascript]
categories: [development]
---

Javascript



## 노드 선택 방법 개선하기

아래와 같은 코드는 매번 Id를 입력해줘야 하고, 이를 다시 js에서 일일이 호출해야하는 불편함이 있다.

```html
<div>
    <input id='txt-x' type="text" value="0" dir="rtl"/>
    +
    <input id='txt-y' type="text" value="0" dir="rtl"/>
    <input id='btn-add' type="button" value="=" />
    <input id='txt-sum' type="text" value="0" readonly dir="rtl"/>
</div>
```

```javascript
window.addEventListener("load", function(){
    let textX = document.getElementById('txt-x')
    let textY = document.getElementById('txt-y')
    let btnAdd = document.getElementById('btn-add')
    let txtSum = document.getElementById('txt-sum')
    btnAdd.onclick = function() {
        txtSum.value = parseInt(textX.value) + parseInt(textY.value)
    }
})
```

그러므로 울타리에 Id를 하나만 지정하고 **하위 노드를 찾는 방식**으로 바꿔보자.

\+ `.getElementByTagName()` : 해당하는 태그를 모두 가져온다. 리스트를 반환

\+ `.getElementsByClassName()` : 해당하는 클래스를 모두 가져온다. 리스트를 반환

\+ `.textContent` : innerText와 동일. 해당 태그의 text를 가져온다.



### 방법 1. 하위 엘리먼트 선택

```html
<section>
    <h1>Ex1 : 계산기 프로그램</h1>
    <div>
        <input id='txt-x' type="text" value="0" dir="rtl"/>
        +
        <input id='txt-y' type="text" value="0" dir="rtl"/>
        <input id='btn-add' type="button" value="=" />
        <input id='txt-sum' type="text" value="0" readonly dir="rtl"/>
    </div>
</section>
```

이 텍스트에서 id를 일일이 가져오는 것은 번거로운 일이다. 그러므로 section에 id를 주고, 이를 통해 접근하는 방식을 택하자.

```javascript
window.addEventListener("load", function(){
    let section2 = document.getElementById("section2")
    let inputs = section2.getElementsByTagName("input")

    let textX = inputs[0]
    let textY = inputs[1]
    let btnAdd = inputs[2]
    let txtSum = inputs[3]
}
```



#### 방법 2. id 대신 class를 사용

하지만 위 방법 역시 문제가 있다. 배열로 처리할 땐 index로 접근하기 때문에 html을 수정하기가 번거롭다는 것이다. 또한 id는 그 페이지에서 고유한 값이 되어야 한다. 그렇기에 id 대신 class로 속성을 변경하여 관리하자.

```html
...
<input class='txt-y' type="text" value="0" dir="rtl"/>
...
```

```javascript
let section2 = document.getElementById("section2")
...
let txtY = section2.getElementsByClassName("txt-y")[0]
...
```

이때 클래스는 여러 개를 가져오기 때문에 배열을 반환한다. index 설정에 주의하자.





#### 참고

- [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)