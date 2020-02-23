---
comments: true
title: 컴파일러와 인터프리터의 차이는? what is the difference between compilers and interpreters?
published: false
updated: 2020-1-29
tags: [compiler, interpreter]
categories: [computer science]
---





### django DB

장고를 실행하면 자동으로 sqlite3를 기본 데이터 베이스로 만듭니다. 이 DB는 로컬에서 서버 실행과 동시에 실행이 되는데, 저희가 원하는 것은 로컬 DB가 아닌 AWS에 올린 DB와 연결하는 것입니다. 이를 위한 준비사항을 정리했습니다.



### mariaDB 설치

다운로드 [링크](https://downloads.mariadb.org/mariadb/)로 들어가 맞는 버전을 설치합니다. development series에 있는 것보다는 stable series를 다운 받습니다.

다운로드 파일 실행을 통해 설치를 마무리 짓습니다.



### Python MariaDB 설치

MariaDB를 사용하기 위해선 mysql 모듈을 설치해야 합니다. 아래 명령어를 입력하여 설치를 진행합니다.

```bash
$ pip install libmysqlclient-dev

# 에러 시 아래 코드로

$ pip install mysqlclient
```

두 명령어로도 설치가 안 된다면 다른 방법을 설치해야 합니다.

이 [링크](https://www.lfd.uci.edu/~gohlke/pythonlibs/#mysqlclient)로 들어간 뒤, Mysqlclient 중 현재 버전에 맞는 것을 설치합니다.

cp38은 CPython 3.8 버전을 의미합니다. `python -V`으로 버전을 확인한 뒤 적절한 파일을 다운받습니다.

이후 아래 명령어를 실행하여 설치를 진행합니다.

```bash
$ pip install [파일 이름]
# 가령 pip install mysqlclient‑1.4.6‑cp38‑cp38‑win_amd64.whl
```



### Django에서 MariaDB로 접근

이제 settings.py에서 DATABASES 정보를 바꿔야 합니다. default로 sqlite3가 설정되어 있는 것을 확인할 수 있습니다.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

이를 외부 DB에 연결하려면 다음과 같이 설정을 바꿔야 합니다.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'db-name',  # 만든 DB의 이름을 넣습니다.
        'USER': 'db-user-name', # DB 생성 시 설정한 ID
        'PASSWORD': 'db-password', # DB 생성 시 설정한 Password
        'HOST': 'db-adress', # 공백일 시 default인 localhost 
                             # 외부 DB에 접근하려면 IP를 적어야 합니다.
                             # ex) 127.13.0.12 
        'PORT': 'port-number' #공백일 시 default인 3306
        'OPTIONS': {'charset': 'utf8mb4'},
    }
}
```

- 한글을 사용하기 위해 다음의 옵션을 넣어줍니다.
  - 이때 table의 인코딩 옵션도 함께 맞춰야 합니다.



연동된 DB를 django가 초기화 할 수 있도록 다음의 명령을 적어야 합니다.

```python
$ python manage.py makemigrations
$ python manage.py migrate
```

이후 django에서 기본으로 제공하는 테이블들이 생성됩니다.

```
auth_group
auth_group_permissions
auth_permission
auth_user
auth_user_groups
auth_user_user_permissions
django_admin_log
djang_content_type
django_migrations
django_session
```



### DB의 테이블을 models.py로 가져오기

django는 class를 사용해 ORM을 이용합니다. DB에 저장된 테이블의 ORM을 가져오고 싶다면 아래의 명령어를 입력하면 됩니다.

```bash
$ python manage.py inspectdb > appname/models.py
```

`migration`명령어가 models.py의 변경 사항을 DB에 적용시키는 명령어인 반면,

`inspectdb` 는 DB의 스키마를 models.py로 가져오는 명령어입니다.







### Model을 dump 해 json 으로 만들기

현재 DB의 데이터를 json으로 dump하려면 아래 명령어를 입력해야 합니다.

```bash
$ python manage.py dumpdata [app_name].[model_name] --indent [INDENT] > [fixture_name].json
```

이를 실제로 적용하면 다음의 코드가 됩니다.

```bash
$ python manage.py dumpdata articles.auther --indent 4 > author.json
```

하지만 인코딩의 문제로 한글이 제대로 나오질 않습니다. 그래서 이를 수정하기 위해 다음의 과정을 거칩니다.

```python
import json

with open('author.json', 'r', encoding='utf-8-sig') as file:
    data = json.load(file)

with open('author.json', 'w', encoding='utf-8-sig') as file:
    json.dump(data, file, indent='\t', ensure_ascii=False)
```

다음과 같은 구조로 JSON 파일이 만들어지게 됩니다.

```json
[
	{
		"pk": 1,
       	"model": "articles.author",
		"fields": {
			"articleName": "제목",
			"bad": 32,
			"good": 122,
			"regdate": "2019-12-12"
		}
	}
]
```







### JSON을 DB로 load 하기

반대로 JSON 파일을 DB에 한 번에 넣을 수도 있습니다. 위의 JSON 처럼 구조를 만들어 준 뒤, 앱 폴더 아래 `fixtures`라는 폴더를 만들고 이 안에 json 확장자로 저장합니다. 이후 다음의 명령어를 통해 DB에 집어 넣습니다.

```bash
$ python manage.py loaddata [app_name]/[file_name]
```

실제 예시는 다음과 같습니다.

```bash
$ python manage.py loaddata author.json
```

- 설치된 앱이 하나인 경우에는 app_name을 쓰지 않아도 됩니다.
- 앱이 여러 개일 경우 다음과 같이 작성하면 됩니다.

```bash
$ python manage.py loaddata articles/author.json
```



