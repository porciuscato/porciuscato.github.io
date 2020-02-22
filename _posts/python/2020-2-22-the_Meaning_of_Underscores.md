---
comments: true
title: The Meaing of Underscores in Python. 파이썬에서 언더바, 언더스코어의 의미
published: false
updated: 2020-2-22
tags: [python, underscore]
categories: [development]
---

python에서 언더스코어, underscore의 의미가 무엇인지 알아봅시다.



#### \* 이 글은 Dan Bader의 글 [The Meaing of Underscores in Python](https://dbader.org/blog/meaning-of-underscores-in-python)을 번역한 글입니다.



# 파이썬에서 언더스코어(Underscores)의 의미

파이썬에는 싱글, 더블 언더스코어("duncer")에 대한 다양한 의미와 네이밍 컨벤션이 있습니다. 이를 통해 네임 맹글링(name mangling)이 어떻게 동작하는지, 그것이 클래스에 어떤 영향을 끼치는지 알아봅시다.

싱글 혹은 더블 언더스코어는 파이썬 변수와 메소드 이름에 있어 의미를 가집니다. 어떤 것들은 그저 컨벤션에 불과하기도 하고 프로그래머에게 힌트가 되기도 합니다. 어떤 것들은 파이썬 인터프리터에 의해 강제되기도 합니다.

'파이썬 변수와 메소드 이름에서 싱글과 더블 언더스코어는 무슨 의미일까?'를 궁금해하시는 여러분들을 위해, 글을 적어보았습니다.

이 글에서 저는 아래의 5가지 언더스코어 패턴과 네이밍 컨벤션, 그리고 그들이 어떻게 파이썬 프로그램에 영향을 끼치는지 서술하겠습니다.

- Single Leading Underscore: `_var`
- Single Trailing Underscore: `var_`
- Double Leading Underscore: `__var`
- Double Leading and Trailing Underscore: `__var__`
- Single Underscore: `_`

이 글의 맨 밑으로 가시면 이들에 대한 요약과 짧은 튜토리얼 비디오가 있습니다.

그러면 







## 📓 파이썬 언더스코어의 네이밍 패턴과 요약

| Pattern                                    | Example   | Meaning                                                      |
| ------------------------------------------ | --------- | ------------------------------------------------------------ |
| **Single Leading Underscore**              | `_var`    | Naming convention indicating a name is meant for internal use.  Generally not enforced by the Python interpreter (except in wildcard  imports) and meant as a hint to the programmer only. |
| **Single Trailing Underscore**             | `var_`    | Used by convention to avoid naming conflicts with Python keywords. |
| **Double Leading Underscore**              | `__var`   | Triggers name mangling when used in a class context. Enforced by the Python interpreter. |
| **Double Leading and Trailing Underscore** | `__var__` | Indicates special methods defined by the Python language. Avoid this naming scheme for your own attributes. |
| **Single Underscore**                      | `_`       | Sometimes used as a name for temporary or insignificant variables  (“don’t care”). Also: The result of the last expression in a Python  REPL. |



## 📺 언더스코어 패턴 - 튜토리얼 비디오

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/ALZmCy2u0jQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

