---
comments: true
title: markdown 들여쓰기, indentation
published: 2020-2-20
updated: 2020-2-20
tags: [markdown]
categories: [development]
---

markdown에서 들여쓰기 하기



## 마크다운 들여쓰기

&nbsp;&nbsp;마크다운을 작성할 때 띄어쓰기 두 번을 입력하면 로컬에서는 마치 들여쓰기가 된 것처럼 보입니다. 하지만 깃헙에 푸쉬를 하면 전혀 들여쓰기가 되어있지 않은 걸 볼 수 있습니다.

&nbsp;&nbsp;들여쓰기를 하기 위해선 `&nbsp;` 를 입력해야 합니다.

&nbsp;&nbsp;마크다운은 들여쓰기를 지원하지는 않지만 html을 지원하기 때문에 공백문자인 `&nbsp;`(Non-breaking space, 줄바꿈 없는 공백)를 사용하는 것입니다.

```
&nbsp;&nbsp;이렇게 작성하면 들여쓰기와 같은 효과를 보입니다.
```

