---
comments: true
title: javascript의 node와 element
published: false
updated: 2020-3-7
tags: [javascript]
categories: [development]
---

javasciprt의 node와 element에 대해 알아보자



## node

html 문서는 load 되면서 트리 구조를 형성한다. 이때 노드는 트리의 구성요소로서의 노드다. 이들은 서로 포함관계를 가지며 부모/자식 관계라 부른다. 

이때 노드는 주석, text 모두를 포함한다. html 태그만 자식인 것은 아니다.

그렇기에 `childNodes`를 사용할 때 다음과 같은 문제가 발생할 수 있다.

```html
<section id="section4">
    <h1>Ex4 : childNodes를 이용한 선택</h1>
    <div class='box'>
        <input type="text" />
        <input type="text" />
    </div>
</section>
```

이때 input 태그를 선택하기 위해 다음과 같은 코드를 작성하면 제대로 동작하지 않는다.

```javascript
let section4 = document.querySelector("#section4")
let box = section4.querySelector('.box')
let input1 = box.childNodes[0]
let input2 = box.childNodes[1]
```

`childNodes`는 div 밑의 텍스트, 즉 공백까지도 하나의 노드로 취급을 한다. 그렇기에 box.childNodes는 [text, input, text, input, text]로서 array다. 

이는 우리가 의도했던 바가 아니다. 우리는 태그만을 선택하고 싶다. 그럴 때 사용하는 것이 `children`이다.

```javascript
let input1 = box.children[0]
let input2 = box.children[1]
```

이때 box.children의 결과는 [input, input] 이다.

그렇다면 node란 무엇인가? 알아보자





----

## Node 인터페이스





### 엘리먼트 노드의 속성 다루기













#### 참고

- [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [w3school](https://www.w3schools.com/jsref/)
- [vanilla-js](http://vanilla-js.com/)
- [newlecture](https://www.youtube.com/watch?v=gxzy_CFqV1M&list=PLq8wAnVUcTFWhQrIXNN6kPYXJA6X2IQM4)
- [w3.org](https://www.w3.org/TR/)