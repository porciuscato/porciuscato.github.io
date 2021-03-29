---
comments: true
title: django decouple 사용하기
published: true
updated: 2021-3-29
tags: [python, django, backend, decoule]
categories: [development]
---

Django framework를 사용하며 secret_key를 숨겨야할 때가 있다.

이때 키를 숨기는 방법에 대해 알아보자.

## python 가상환경

서버는 python 가상환경으로 컨트롤하자.

```bash
virtualenv venv
source venv/Scripts/activate
```

> venv는 가상환경 이름이다. 아무거나 해도 상관없다.
>
> 후에 가상환경을 종료하고 싶다면 deactivate를 입력하면 된다.

## 설치

```bash
pip install python-decouple
```

> pip install decouple 하면 안 된다. 이 패키지와 엄연히 다른 패키지다. import 할 때 이름이 decouple이라 헷갈릴 수 있는데, 만약 decouple을 설치해서 작동하지 않는다면 decouple 패키지를 삭제하자.
>
> `pip uninstall decouple`

## secret_key 저장

django 프로젝트를 시행하면(`django-admin startproject <name>`) root 위치에 manage.py가 생성되는데, 이 파일과 같은 위치에 `.env`파일을 생성한다.

`.env` 파일 안에 사용할 변수의 이름과 값을 띄어쓰기 없이 붙여쓴다.

이때 문자열이라도 따옴표를 붙이지 않는다.

#### 예시

```
DEBUG=True
TEMPLATE_DEBUG=True
SECRET_KEY=REALSECRETKEY
DATABASE_URL=mysql://user:password@localhost/name
```



## 사용하기

그리고 소스 코드로 돌아가 decouple의 confing를 가져와 사용하자.

```python
from decouple import config

DEBUG = config('DEBUG', cast=bool)
SECRET_KEY = config('SECRET_KEY')
```

