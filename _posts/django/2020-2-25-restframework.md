---
comments: true
title: django로 REST 서버 만들기
published: false
updated: 2020-2-25
tags: [python, django, backend, restframework]
categories: [development]
---

django로 REST Framework를 만들어봅시다.



# 설치

pip를 사용하여 다운을 받습니다.

```bash
$ pip install djangorestframework
```

django를 실행합니다.

```bash
$ django-admin startproject example
```

app을 추가합니다.

``` bash
$ cd example
$ django-admin startapp accounts
```

`exmaple/settings.py`에 `INSTALLED_APPS`에 설치한 django rest framework와 앱을 추가합니다.

```
INSTALLED_APPS = [
    'accounts',
    'rest_framework',
    ...
]
```

데이터베이스와 싱크를 맞춥니다.

```bash
$ python manage.py migrate
```

관리자 계정을 하나 만듭니다.

```bash
$ python manage.py createsupersuer --email admin@admin.com --username admin
```



# Model

`accounts/models.py`에 모델을 만듭니다. 

```python
from django.db import models

class Human(models.Model):
    name = models.CharField(max_length=60)
    alias = models.CharField(max_length=60)

    def __str__(self):
        return self.name
```

모델의 수정사항을 저장합니다.

```bash
$ python manage.py makemigrations
```

수정사항을 DB에 적용시킵니다.

```bash
$ python manage.py migrate
```

만든 모델을 admin 창에서 볼 수 있도록 설정합니다. `accounts/admin.py`에 등록합니다.

```python
from django.contrib import admin
from .models import Human

admin.site.register(Human)
```



# Serializer

serializer를 사용하기 위해 `accounts/serializers.py`를 만들고 등록합니다.

```python
from rest_framework import serializers
from .models import Human

class HumanSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Human
        fields = ('name', 'alias',)
```



# Views

viewset을 사용해 DB의 모든 Human을 보여줍니다. `accounts/views.py`에 알려줍니다.

```python
from django.shortcuts import render
from rest_framework import viewsets
from .serializers import HumanSerializer
from .models import Human

class HumanViewSet(viewsets.ModelViewSet):
  	serializer_class = HumanSerializer
    queryset = Human.objects.all().order_by('name')    
```



# URLs

API 요청은 accounts 앱에서 처리하게 만들게 위해 이를 메인 url에 알려줍니다. `example/urls.py`에 다음과 같이 작성합니다.

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('accounts.urls')),
]
```

이제 `accounts/urls.py`를 만들고 router를 생성합니다.

```python
from django.urls import include, path
from rest_framework import routers
from . import views

router = routers.DefaultRouter()
router.register(r'human', views.HumanViewSet)

# automatic URL routing
urlpatterns = [
    path('', include(router.urls)),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework')),
]
```



## admin page 등록

생성한 모델을 admin 페이지에서 수정이 가능하게 만들 수 있습니다.

앱의 admin.py에 코드를 적습니다.

`accounts/admin.py`

```python
from django.contrib import admin
from .models import Human

class HumanAdmin(admin.ModelAdmin):
    list_display = ('pk', 'name', 'alias', )

admin.site.register(Human, HumanAdmin)
```



# 서버 실행

서버를 실행하면 rest framework를 확인할 수 있습니다.

```bash
$ python manage.py runserver
```







#### 참고

- [medium 글](https://medium.com/@BennettGarner/build-your-first-rest-api-with-django-rest-framework-e394e39a482c)

+ [django api 참고 글](https://simpleisbetterthancomplex.com/tutorial/2018/02/03/how-to-use-restful-apis-with-django.html)