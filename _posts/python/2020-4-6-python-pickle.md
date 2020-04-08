---
comments: true
title: python pickle
published: 2020-4-6
updated: 2020-4-6
tags: [python, pickle]
categories: [development]
---

python pickle 모듈을 사용해 데이터를 그대로 저장해보자.



## 파일 저장 및 불러오기

파이썬으로 파일을 저장하거나 읽어올 땐 다음과 같이 코드를 작성한다.

```python
text = "hello"

# text를 hello.txt 파일에 저장한다.
with open("hello.txt", 'w') as f:
  f.write(text)

# hello.txt 파일을 읽어와 text 변수에 저장한다.
with open('hello.txt', 'r') as f:
  text = f.read()
```

그런데 이때 입출력되는 데이터는 문자열이어야 한다. 그렇기에 list, dictionary 등을 담을 수 없다.

다음과 같은 코드를 작성하면 에러가 발생한다.

```python
test_list = [1, 2, 3, 4]

with open("test.txt", 'w') as f:
  f.write(test_list)
```

pickle 모듈을 사용하면 리스트를 그대로 저장할 수 있게 된다. 사용법은 아래와 같다.



## pickle 사용법

```python
import pickle
my_list = ['a','b','c']
 
## Save pickle
with open("data.pickle","wb") as fw:
    pickle.dump(my_list, fw)
 
## Load pickle
with open("data.pickle","rb") as fr:
    data = pickle.load(fr)
print(data)
#['a', 'b', 'c']
```

사용법은 간단하다. 

- 저장할 땐 `pickle.dump(데이터, 파일)`
- 불러올 땐 `pickle.load(파일)` 을 하면 된다.

주의할 점은 1

1) 확장자를 `.pickle`로 선언한다. (pickle이 아니어도 읽고 쓰기에 문제는 없으나 pickle 모듈을 사용하라는 것을 명시적으로 표시하기 위해 확장자를 알려줘야 한다.) 

2) 바이너리 형식으로 다루기 때문에 저장할 땐 `wb`, 읽을 땐 `rb` 옵션을 준다. 

