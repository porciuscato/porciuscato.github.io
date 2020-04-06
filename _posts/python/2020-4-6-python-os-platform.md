---
comments: true
title: python pickle
published: 2020-4-6
updated: 2020-4-6
tags: [python]
categories: [development]
---

python platform 모듈을 사용해 현재 코드가 동작하는 컴퓨터의 운영체제를 알아보자.



```python
import platform

# 현재 운영체제가 string으로 반환된다.
print(platform.system())
```

윈도우와 리눅스 환경에 따라 설정이나 경로가 달라질 수 있다. 윈도우용에서 개발한 코드가 다른 운영체제에서 작동하지 않을 수 있다. 그러므로 운영체제에 따라 미묘하게 설정들을 바꿀 수 있어야 한다.