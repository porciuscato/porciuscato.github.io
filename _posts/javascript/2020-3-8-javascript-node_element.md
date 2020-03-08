---
comments: true
title: javascript로 CSS 속성 다루기
published: 2020-3-8
updated: 2020-3-8
tags: [javascript, CSS]
categories: [development]
---

javasciprt로 CSS 속성을 다뤄보자



## CSS 속성 바꾸기

#### 명명 규칙

CSS 속성을 다룰 때 주의할 점이 있다. `-`은 JS 예약어이기 때문에 변수로서 그대로 쓸 수 없다. 가령 이런 코드는 가능하지 않다.

```javascript
let img = querySelector(".img")
img.style.border-color = "red"
```

`-`을 사용하기 위해선 다음과 같이 써야 한다.

```javascript
img.style["border-color"] = "red"
```

혹은 이렇게도 가능하다.

```javascript
img.style.borderColor = "red"
```

