---
comments: true
title: python deque
published: 2020-5-15
updated: 2020-5-15
tags: [python, deque]
categories: [development]
---

python deque 사용하기



## deque

파이썬의 기본 자료형인 list보다 빠르다고 알려진 deque다. 양쪽 모두에서 값을 넣고 빼는데 O(1)의 시간 복잡도를 낸다. 반면 list는 pop(0)와 insert(0, v) 등의 연산에서 O(n)의 속도를 낸다. 그렇기에 deque가 더 빠르다.



사용법은 다음과 같다.

```python
from collections import deque

# deque에 리스트를 넣어서, 기본 자료형인 list를 deque로 바꾼다.
que = deque([1, 2, 3])
```

만약 최대 값을 설정한다면, 추가 연산으로 덱이 꽉 찼을 때 반대 방향의 원소가 제거된다.



### 메소드

- append(x)
  - 오른쪽에 원소 추가
- appendleft(x)
  - 왼쪽에 원소 추가

- clear()
  - 모든 원소 삭제
- copy()
  - 얕은 복사를 만든다.
- count(x)
  - x의 값과 같은 것의 갯수를 반환한다.
- extend(iterable)
  - 리스트를 덱의 오른쪽에 붙인다.
- extendleft(iterable)
  - 리스트를 덱의 왼쪽에 붙인다.
- insert(i, x)
  - i 위치에 x를 넣는다.

- pop()
  - 오른쪽 값을 제거하여 반환한다.
- popleft()
  - 왼쪽 값을 제거하여 반환한다.
- remove(value)
  - 첫 번째 value 값을 제거한다.
- reverse()
  - 리스트를 뒤집는다.
- rotate(n=1)
  - 모든 원소를 n 만큼 오른쪽으로 옮긴다. 음수라면 왼쪽으로 옮긴다.