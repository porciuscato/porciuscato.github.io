---
comments: true
title: python dir
published: false
updated: 2020-2-22
tags: [python, os, sys]
categories: [development]
---

python dir은 무엇인가



### dir function

&nbsp;&nbsp; 특정 모듈이나 함수가 가진 속성과 메소드를 모두 볼 수 있는 함수로써 python3를 사용하다보면 참으로 유용한 내장함수입니다. documentation을 보지 않더라도 dir 만으로도 많은 정보를 얻을 수 있죠.

&nbsp;&nbsp;사용법은 다음과 같습니다.

```
dir({object})
```

object 부분에 확인이 필요한 모듈을 넣으면 사용할 수 있는 속성, 및 함수들이 나오게 됩니다.

가령, `[]`(List)를 넣으면 아래와 같은 결과가 나옵니다.

```python
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

&nbsp;&nbsp;`dir()`은 List를 return 합니다. List를 사용할 때 

