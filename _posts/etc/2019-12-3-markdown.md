---
comments: true
title: 마크다운 작성법
published: 2019-12-3
updated: 2019-12-3
tags: [markdown]
categories: "computer science"
---
- 마크다운은 간단히 문서를 작성할 때 아주 편리한 도구입니다. 사용법을 익히면 쉽고 빠르게 구조를 갖춘 문서를 만들 수 있습니다. 마크다운의 간단한 문법들을 정리해 보았습니다.

# 마크다운 작성법

## 1. 문법

### 1.1 헤더 Headers

`#` 를 사용. 1~ 6개까지 가능

<예시>
```html
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

<결과>

# H1

## H2

### H3

#### H4

##### H5

###### H6



### 1.2 Block Quote

`>` 블럭 인용문자를 사용. `#` 와는 달리 제한이 없다. 원하는 만큼 쓸 수 있다.

<예시>

```
> 1
>> 2
>>> 3
>>>> 4
>>>>> 5
>>>>>> 6
>>>>>>> 7
```

<결과>

> 1
> > 2
> > > 3
> > > > 4
> > > >
> > > > > 5
> > > > > > 6
> > > > > >
> > > > > > > 7

인용 부분 안에서도 markdown 문법을 동일하게 사용할 수 있다.

<예시>

```
> # 제목
> - 내용
```

<결과>

> # 제목
> - 내용



### 1.3 목록

#### 1.3.1 순서있는 목록

숫자와 점을 사용한다.

<예시>

```
1. 첫번째
2. 두번째
3. 세번째
```

<결과>

1. 첫번째
2. 두번째
3. 세번째



#### 1.3.2 순서없는 목록

`-` , `*`, `+` 를 사용. 세 가지를 섞어 써도 결과는 같다.

<예시>

```
- 하나
* 둘
+ 셋
```

<결과>

- 하나
- 둘
- 셋

<예시>

```
- 하나
    - 둘
        - 셋
            - 넷
                - 다섯
```

<결과>  (셋 이후로는 같다.)

- 하나
	- 둘
		- 셋
		  - 넷
		    - 다섯



- \- \+ \* 을 그대로 사용하려면 앞에 \\ 을 붙여주면 된다.

<예시>

```
\- \+ \* \\
```

<결과>

\- \+ \* \\



### 1.4 HTML 태그

HTML 태그를 그대로 적용할 수 있다. 

<예시>

```
<p><strong>strong</strong></p>
<p><small>small</small></p>
<p><sup>sup</sup></p>
<p><sub>sub</sub></p>
```

<결과>

<p><strong>strong</strong></p>
<p><small>small</small></p>
<p><sup>sup</sup></p>
<p><sub>sub</sub></p>

---

pre 태그는 입력한 그대로 보여준다.

code 태그는 안에 있는 내용이 코드임을 알려준다.

<예시>

```
<pre> 
여기에 쓰면 
	그대로 출력이 됩니다.
<code>
window.document.console.log('console log')
</code>
</pre>
```

<사용결과>

<pre> 
여기에 쓰면 
	그대로 출력이 됩니다.
<code>
window.document.console.log('console log')
</code>
</pre>

### 1.5 수평선

아래 모두 수평선을 만든다. asterisk 혹은 dash를 3개 이상 연속으로 쓰면 수평선이 만들어진다.

<예시>

```
***
---
*****
---------
* * * * *
- - - - - - -
<hr/>
```

<결과>

***
---
*****
---------
* * * * *
- - - - - - -
<hr/>

=> HTML 태그가 바로 적용이 되기 때문에 `hr 태그`도 수평선을 만든다.



### 1.6 링크

- 자동연결 - URL 혹은 이메일에 바로 링크를 넣을 수 있다. `<링크>`

<예시>

```
<https://www.google.com>
<mpcato@naver.com>
```

<결과>

<https://www.google.com>

<mpcato@naver.com>



- 인라인 링크: `[p](링크)` -> 다른 파일로 이동할 때

<예시>

```
[title](./mbti/index.html)
[vuejs](./vuejs.md)
```

<결과>

[title](./mbti/index.html)

[vuejs](./vuejs.md)



- 인라인링크 -> 동일 파일 내 특정 태그로 이동하고 싶을 때

<예시>

```
[제목](#마크다운-작성법)
```

<결과>

[제목](#마크다운-작성법)



- 인라인링크 -> 다른 파일 내 특정 태그로 이동하고 싶을때

<예시>

```
[vuejs](./vuejs.md#Vue.js)
```

<결과>

[vuejs](./javascript.md#javascript)



- 참조링크

<예시>

```
[link keyword][id]
[id]: URL "Optional Title here"

Link: [Google][여기로]
[여기로]: https://google.com "Go google"
```

<결과>

Link: [Google][여기로]

[여기로]: https://google.com "Go google"



> 인라인 링크는 대괄호 옆 소괄호 안에 직접 URL 링크를 거는 방식이다.
>
> 반면 참조링크는 마치 링크를 변수화 한 것처럼 대괄호 옆 대괄호 안에 연결할 링크를 변수로써 설정하는 것이다. 변수의 링크를 정의할 땐 사용할 곳의 상하 모두 가능하다.



#### 참고

- [ihoneymon 님의 리포](https://gist.github.com/ihoneymon/652be052a0727ad59601 )

- [John Gruber](https://daringfireball.net/projects/markdown/syntax)
