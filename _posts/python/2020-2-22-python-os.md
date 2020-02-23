---
comments: true
title: python os에 대해 알아보자
published: false
updated: 2020-2-22
tags: [python, os, sys]
categories: [development]
---

python 의 os의 구조를 분석해봅시다.



# os 사용법

먼저 os 모듈을 import 합니다.

`dir()`과 `help()` 함수로 사용할 수 있는 속성이 무엇이 있나 확인할 수 있습니다.

```python
import os

print('******************** dir(os)  ********************')
print(dir(os))
print()
print('******************** help(os) ********************')
print(help(os))
```

이후 출력 결과를 확인하면 다음과 같습니다.

