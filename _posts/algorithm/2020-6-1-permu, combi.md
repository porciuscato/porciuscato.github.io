---
title: 순열 조합 코드를 작성하는 법과 라이브러리 이용법
published: false
updated: 2020-6-1
tags: [python, algorithm, combination, permutation]
categories: [development]
---

순열 조합을 코드로 작성해보자. 작성한 코드보다 더 빠른 라이브러리 이용 방법도 알아보자.



## 조합

#### 1) 직접 작성

```python
def combination(origin, aim, array: list=[], depth=0, last=0):
    if depth == aim:
        pass
    else:
        for i in range(last, len(origin)):
            arr = array[:]
            arr.append(origin[i])
            combination(origin, aim, arr, depth + 1, i + 1)
```

#### 2) 라이브러리 이용

```python
from itertools import combinations

for i in combinations(array, num):
  pass  # i는 조합 결과다.
```



#### 3) 두 코드의 속도 비교

```python
from itertools import combinations
from time import time

some = [i for i in range(22)]


def combination(origin, aim, array: list=[], depth=0, last=0):
    if depth == aim:
        pass
    else:
        for i in range(last, len(origin)):
            arr = array[:]
            arr.append(origin[i])
            combination(origin, aim, arr, depth + 1, i + 1)


start = time()
combination(some, 11)
print(time() - start)
start = time()
for i in combinations(some, 11):
    pass
print(time() - start)
```

```bash
>>> 3.401883125305176
>>> 0.07300019264221191
```

**라이브러리가 월등히 빠르다.**



## 순열

#### 1) 직접 작성

```python
def permutation(origin, aim, array=[], depth=0, visited=[]):
    if depth == 0:
        visited = [0] * len(origin)
    if depth == aim:
        pass
    else:
        for i in range(len(origin)):
            if not visited[i]:
                arr = array[:]
                arr.append(origin[i])
                visited[i] = 1
                permutation(origin, aim, arr, depth + 1, visited)
                visited[i] = 0
```

#### 2) 라이브러리

```python
from itertools import permutations

for i in permutations(array, chosen):
    pass
```

#### 3) 비교

```python
from itertools import permutations
from time import time

SIZE = 15
chosen = 6
array = [i for i in range(SIZE)]


def permutation(origin, aim, array=[], depth=0, visited=[]):
    if depth == 0:
        visited = [0] * len(origin)
    if depth == aim:
        pass
    else:
        for i in range(len(origin)):
            if not visited[i]:
                arr = array[:]
                arr.append(origin[i])
                visited[i] = 1
                permutation(origin, aim, arr, depth + 1, visited)
                visited[i] = 0
                

start = time()
permutation(array, chosen)
print(time() - start)

start = time()
for i in permutations(array, chosen):
    pass
print(time() - start)
```

```bash
>>> 4.294824838638306
>>> 0.33490562438964844
```

**라이브러리가 월등히 빠르다.**

=> 라이브러리를 쓰자.

