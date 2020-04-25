---
comments: true
title: django rest framework serializer 만들기
published: false
updated: 2020-2-25
tags: [python, django, backend, restframework, serializer]
categories: [development]
---

django rest framework serializer를 사용해봅시다.

이 글은 Django Rest Framework의 튜토리얼을 번역하는 형식으로 작성되었습니다.



# 환경설정

파이썬 가상환경에서 실행하기 위해 다음의 명령어를 입력합니다. 윈도우 기반입니다.

```bash
$ virtualenv venv
$ source venv/Scripts/activate
```

여기에 django 실행을 위한 패키지를 설치합니다.

```bash
$ pip install django
$ pip install djangorestframework
$ pip install pygments  # 코드 하이라이팅을 위해 사용합니다.
```

> 가상환경을 종료하려면 `deactivate`를 타이핑하세요.



# 시작하기

새로운 프로젝트 tutorial을 만들고, 그곳에 앱 snippets를 만듭니다.

```bash
$ django-admin startproject tutorial
$ cd tutorial
$ django-admin startapp snippets
```

새로 추가한 앱을 `tutorial/settings.py`에 알려줘야 합니다.

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
    'snippets.apps.SnippetsConfig',
]
```



# 모델 만들기

`Snippet` 모델을 만들어봅시다. `snippets/models.py` 파일을 만들고 아래 코드를 작성합니다.

```python
from django.db import models
from pygments.lexers import get_all_lexers
from pygments.styles import get_all_styles

LEXERS = [item for item in get_all_lexers() if item[1]]
LANGUAGE_CHOICES = sorted([(item[1][0]), item[0]] for item in LEXERS)
STYLE_CHOICES = sorted([(item, item) for item in get_all_styles()])

class Snippet(models.Model):
    created = models.DateTimeField(auto_now_add=True)
    title = models.CharField(max_length=100, blank=True, default='')
    code = models.TextField()
    linenos = models.BooleanField(default=False)
    language = models.CharField(choices=LANGUAGE_CHOICES, default='python', max_length=100)
    style = models.CharField(choices=STYLE_CHOICES, default='friendly', max_length=100)

    class Meta:
        ordering = ('created',)
```

이제 만든 모델을 DB와 동기화시킵니다.

```bash
$ python manage.py makemigrations snippets
$ python manage.py migrate
```



# Serializer 만들기

웹 API는 DB의 정보를 json형식으로 serialize해 전달합니다. 이를 위해 Snippet 모델에 해당하는 serializer를 작성합니다. 위치는 `snippets/serializers.py`입니다.

```python
from rest_framework import serializers
from snippets.models import Snippet, LANGUAGE_CHOICES, STYLE_CHOICES

class SnippetSerializer(serializers.Serializer):
    id = serializers.IntegerField(read_only=True)
    title = serializers.CharField(required=False, allow_blank=True, max_length=100)
    code = serializers.CharField(style={'base_template': 'textarea.html'})
    linenos = serializers.BooleanField(required=False)
    language = serializers.ChoiceField(choices=LANGUAGE_CHOICES, default='python')
    style = serializers.ChoiceField(choices=STYLE_CHOICES, default='friendly')

    def create(self, validated_data):
        # 타당한 데이터를 받아 새로운 Snippet 객체를 반환합니다.
        return Snippet.objects.create(**validated_data)

    def update(self, instance, validated_data):
        instance.title = validated_data.get('title', instance.title)
        instance.code = validated_data.get('code', instance.code)
        instance.linenos = validated_data.get('linenos', instance.linenos)
        instance.language = validated_data.get('language', instance.language)
        instance.style = validated_data.get('style', instance.style)
        instance.save()
        # 타당한 데이터를 받아 객체를 수정합니다.
        return instance
```

윗 부분에서 클래스의 필드들을 정의했습니다. 메소드들은 인스턴스를 생성하고 수정하여 객체를 반환합니다.

serializer 클래스는 django의 form 클래스와 유사합니다. form처럼 required, max_length, default 등 validation flags을 가지고 있습니다. 

field flags는 특정 환경에서 어떻게 보여져야하는지 컨트롤할 수도 있습니다. 위에 `{'base_template': 'textarea.html'}`은 django form에서 `widget=widget.Textarea`와 같습니다. 





## admin 페이지에 모델 등록하기

admin 페이지에서 만든 모델을 직접 관리할 수 있습니다. 이를 위해선 아래와 같이 작성한 모델을 등록해야합니다. `앱/admin.py`에 코드를 적습니다.

```python
from django.contrib import admin
from .models import Example # 작성한 모델들을 가져옵니다.

class ExampleAdmin(admin.ModelAdmin):
  list_display = ('id', 'title', 'regdate',)
 
admin.site.register(Example, ExampleAdmin)
```





#### 참고

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
        # 모든 필드는 fields = '__all__'
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



# 서버 실행

서버를 실행하면 rest framework를 확인할 수 있습니다.

```bash
$ python manage.py runserver
```







#### 참고

- [원문글](https://www.django-rest-framework.org/tutorial/1-serialization/)
