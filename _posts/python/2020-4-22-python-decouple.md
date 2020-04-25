---
comments: true
title: python decouple로 Secret Key를 숨기자.
published: 2020-4-22
updated: 2020-4-22
tags: [python, decouple]
categories: [development]
---

python decouple로 Secret Key를 숨기자



## 키 숨기기

개발을 하다보면 Secret Key를 숨겨야하는 경우가 자주 발생한다.

여러 방법이 있지만 python의 decouple 모듈을 사용해보자.

### 설치

아래 명령어로 설치한다.

```bash
pip install python-decouple
```

### 변수 설정

사용할 변수들을 `settings.ini` 파일로 저장하거나 `.env` 파일로 저장한다.

변수들을 선언할 땐 띄어쓰기 없이 작성하고 문자열도 따옴표 없이 사용하자.

settings.ini 파일로 저장할 땐 반드시 최상단에 `[settings]` 를 써준다.

```
[settings]
DEBUG=True
TEMPLATE_DEBUG=True
SECRET_KEY=REALSECRETKEY
DATABASE_URL=mysql://user:password@localhost/name
```

.env 파일로 저장할 땐 `[settings]` 표시가 필요 없다.

```
DEBUG=True
TEMPLATE_DEBUG=True
SECRET_KEY=REALSECRETKEY
DATABASE_URL=mysql://user:password@localhost/name
```

### 불러오기

Key를 사용할 파일에서 decouple을 불러와 아래와 같이 사용한다.

```python
from decouple import config

DEBUG = config('DEBUG', cast=bool)
SECRET_KEY = config('SECRET_KEY')
```

> 위의 코드처럼 setings.ini 혹은 .env 파일에 저장한 변수를 불러올 땐 config() 함수 내 문자열로서 변수명을 전달한다.

