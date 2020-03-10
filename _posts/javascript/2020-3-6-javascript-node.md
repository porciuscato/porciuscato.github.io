---
comments: true
title: javascript에서 엘리먼트, 노드 다루기
published: false
updated: 2020-3-8
tags: [javascript]
categories: [development]
---

javascript에서 노드와 엘리먼트를 다뤄보자.



## 엘리먼트 선택 방법

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
    let section = document.getElementById("section")
    let inputs = section.getElementsByTagName("input")

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



#### 방법 3. querySelector

`querySelector` 와 `querySelectorAll`을 사용하면 css selector를 사용할 수 있다.

```javascript
let section3 = document.getElementById("section3")
...
let txtY = section3.querySelector(".txt-y")
...
```

태그가 name 속성을 가지는 경우도 생각해보자.

```html
<input name='x' type="text" value="0" dir="rtl"/>
```

이를 querySelector 로 가져오기 위해서 다음과 같이 쓸 수 있다.

```javascript
let txtX = section3.querySelector("input[name='x']")
```



## 현재 Document에 노드 추가/삭제 하기

### 추가

노드를 생성해도 DOM에 추가하지 않으면 브라우저 상에 보이지 않는다. 추가는 `append` 혹은 `insert`로 가능하다.

생성 자체는 `createElement` 혹은 `createTextNode`로 가능하다. 이로써 메모리에 load는 됐지만 DOM에는 없는 상태기에 보이지 않는다.

DOM에 추가하기 위해선 특정 노드를 선택하고(자식을 가질 수 있는 노드), `append`, `appendChild`를 사용한다.

```html
<div>
    <input type="text" class="input-text">
    <input type="button" value="추가" class="add-button">
    <input type="button" value="삭제" class="remove-button">
</div>
<ul class="menu-list"></ul>
```

ul 태그에 a 태그를 가진 li 태그를 추가하기 위해 다음과 같이 쓸 수 있다.

#### appendChild

```javascript
let a = document.createElement('a')
let li = document.createElement('li')
let txtnode = document.createTextNode(inputText.value)
a.appendChild(txtnode)
li.appendChild(a)
menuList.appendChild(li)
```

하지만 이는 appendChild를 세 번이나 호출하기에 좋지 않다. 한 번에 할 수 있는 방법도 있다. 그것은 `innerHTML`을 사용하는 방법이다.

#### innerHTML

```javascript
menuList.innerHTML += '<li><a href="#">' + inputText.value + '</a></li>'
```

이 역시도 문제가 있다. 받는 형식이 string이기 때문에 이를 다시 object로 만들어야 한다. 즉 object인 menuList를 string으로 형변환 후, string을 menuList에 붙인다. 그리고 다시 string 전체를 object로 전환한다. 이는 성능 저하로 이어질 수 있기에 좋지 않다. 그러므로 다음과 같은 방법을 사용하자.

#### appendChild + innerHTML

```javascript
let li = document.createElement('li')
li.innerHTML = '<a href="#">' + inputText.value + '</a>'
menuList.appendChild(li)
```

작은 단위에서 innerHTML을 사용했고, 큰 단위에서는 append를 사용했기에 성능을 높일 수 있는 방식이다.

#### append

append를 통해 텍스트, 노드 모두 삽입이 가능하다.



### 삭제

삭제는 크게 두 가지 방식이 있다. 부모로부터 자식을 지우는 경우, 혹은 그 태그를 바로 지우는 경우가 그것이다.

#### removeChild

특정 태그의 부모를 찾아가서 지운다.

```javascript
let sibling = parent.children[0]
parent.removeChild(sibling)
```

> 태그는 html에서 지워지지만 sibling에 대한 참조는 남아있다. 그래서 sibling을 다른 곳에 옮기는 것이 가능하다.

#### remove

굳이 부모를 찾지 않더라도 바로 지울 수 있다.

```javascript
let sibling = parent.children[0]
sibling.remove()
```



## 노드 복제하기

#### cloneNode

`cloneNode(false)`를 하게 되면 해당 태그만 가져온다. true를 하면 자식 노드까지 전부 가져온다.

```javascript
let memuList = section.querySelector('#menu-list')
let cloneList = menuList.cloneNode(true)
```

복제할 게 없을 땐 template 태그를 사용할 수 있다. template의 내용은 화면 상에 보여지지 않는다.

```html
<template>
	<tr>
		<td></td>
        <td><a href=""></a></td>
        <td></td>
    </tr>
</template>
```

이 같은 경우가 있을 때 template을 clone하는 방식은 위와는 다르다.

#### importNode

```javascript
let temp = section.querySelector('template')
let cloneNode = document.importNode(temp.content, true)
```

template이 가지고 있는 content를 모두 deeply 하게 가져오겠다는 것을 의미한다.



## 노드 삽입과 바꾸기

그 전에 한 노드에 대해 그 노드의 부모와 형제, 자식들을 고르는 메소드들을 살펴보자. 좌측에 있는 메소드는 모든 노드를 선택하기 때문에 text node도 범위 안에 포함된다. 엘리먼트만을 선택하려면 우측의 메소드를 사용하자.

| Node 선택 | Element 선택 |
| ---- | ---- |
| parentNode | parentElementNode |
| firstChild | firstElementChild |
| lastChild | lastElementChild |
| previousSibling | previousElementSibling |
| nextSibling | nextElementSibling |

\+ 만약 선택한 노드가 없다면 null이 return 된다.

특정 노드를 선택하여 특정 위치에 넣기 위해서 사용하는 메소드는 `insertBefore`다.  이는 특정한 두 노드의 위치를 바꾸는 메소드다. 혹은 특정한 노드를 생성한 뒤 해당 노드 앞에 추가할 수도 있다.

```html
<tbody>
    <tr>
        <td>1</td>
        <td><a href="1">파이썬</a></td>
        <td>2019-01-25</td>
        <td>newlec</td>
        <td>2</td>
    </tr>
    <tr>
        <td>2</td>
        <td><a href="2">자바스크립트</a></td>
        <td>2019-01-26</td>
        <td>newlec</td>
        <td>1</td>
    </tr>
</tbody>
```

두 위치를 바꾸기 위해선

#### insertBefore

```javascript
let currentNode = tbodyNode.firstElementChild  // 맨 위의 노드를 선택
let nextNode = currentNode.nextElementSibling  // 선택한 노드의 이전 형제를 선택
if (nextNode === null){ // 원하는 노드가 없을 경우 null을 반환
     alert('더 이상 이동할 수 없습니다.')
 }
else{
	tbodyNode.insertBefore(nextNode, currentNode)
}
```

이는 다음의 노드를 빼서 현재 노드 앞에 두는 코드다. 이 메소드는 특정 노드의 앞에만 넣을 수 있다. 이보다 더 직관적인 메소드도 있다.

#### insertAdjacentElement

insertBefore가 부모 노드를 선택한 상태에서 두 자식 노드를 바꾸는 메소드였다면, insertAdjacentElement는 부모 노드를 선택할 필요 없이 바꾸는 것이 가능하다. 위의 else 부분을 다음과 같이 바꾸면 된다.

```javascript
currentNode.insertAdjacentBefore("beforebegin", nextNode)
```

현재 노드의 앞에 다음 노드를 붙이는 것이다. 괄호 안의 위치는 4가지가 가능하다.

```html
<!-- beforebegin -->
<p>
  <!-- afterbegin -->
  foo
  <!-- beforeend -->
</p>
<!-- afterend -->
```

p가 현재 노드다. `beforebegin`과 `afterend`로 p 노드 앞 뒤로 노드 삽입이 가능하다.



## 다중 노드 선택과 일괄삭제 및 자리바꾸기

input 태그 checkbox 타입에서 체크를 하려면 checked='true' 옵션을 주면 된다. 이때 버튼 하나를 클릭했을 때 

```html

```







#### 참고

- [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)

- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)