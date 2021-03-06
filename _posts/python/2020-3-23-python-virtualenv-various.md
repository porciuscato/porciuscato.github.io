---
comments: true
title: 윈도우에서 python 가상환경으로 다양한 버전 다루기
published: 2020-3-23
updated: 2020-3-23
tags: [python, virtualenv]
categories: [development]
---

파이썬으로 다양한 버전의 가상환경을 구축해보자.



## 현재 버전 확인하기

파이썬을 설치할 때 파이썬을 PATH에 추가했다면 다음의 명령어를 통해 현재 버전을 확인할 수 있다.

```bash
$ python -V
```

현재 python 버전은 3.8.2다. 이 버전은 다음의 경로에서 실행된다. 

```
C:\Users\user\AppData\Local\Programs\Python\Python38-32\
```

이는 `제어판/시스템 및 보안/시스템/고급 시스템 설정/환경변수`에서 확인할 수 있다. 필자는 시스템 변수가 아닌 사용자 변수 중 PATH에서 이를 확인한다.

이제 만들고 싶은 가상환경은 3.6.8버전이다. 이를 먼저 설치하자.

## 원하는 버전 다운받기

파이썬 다운 페이지로 간다. [링크](https://www.python.org/downloads/)

원하는 버전의 download 버튼을 클릭한 뒤 다운 받을 수 있는 파일을 선택해야 한다. 현재 운영체제는 64비트이기에 `Windows x86-64 executable installer`를 선택해 다운을 받는다. 이때 설치의 편의를 위해 다운 파일을 실행하면서 `add to PATH`를 꼭 클릭하자.

설치가 완료되면 사용자 변수에 설치한 버전의 경로가 추가되어있는 것을 확인할 수 있다. 



## 버전 확인하기

python을 bash 창에서 실행하면 환경변수를 살피며 해당 명령어를 실행한다. 그러므로 추가된 파이썬 경로들이 많을 경우 원하는 버전을 환경변수 중 가장 위로 올리면 해당 버전이 실행된다. 필자는 3.6.8버전을 맨 위로 올렸다.



## 가상환경 설정하기

그런데 다른 버전을 실행할 떄마다 환경변수의 위치를 변경해주는 것은 번거로운 일이다. 그래서 원하는 버전으로 파이썬 환경변수를 설정한 뒤, 가상환경을 구축하는 방식으로 진행하려 한다.

먼저 원하는 파이썬 버전인지 확인한다.

```bash
$ python -V
```

원하는 버전일 경우 진행하고, 아닐 경우 환경변수를 수정한다.

가상환경을 구축하기 위해 virtualenv를 설치하자.

```bash
# 업그레이드가 안 되어있다면 진행
$ pip install --upgrade pip
# virtualenv 설치
$ pip install virtualenv
```

이제 원하는 디렉터리로 들어가서 가상환경 폴더를 생성한다. 폴더 이름은 `venv368`로 하겠다.

```bash
$ virtualenv venv368
```

이제 가상환경을 실행하자.

```bash
$ source venv368/Scripts/activate
```

그리고 버전을 확인하자.

```bash
$ python -V
```

이제 가상환경을 실행하면 3.6.8 버전으로 실행되는 것을 확인할 수 있다.

글로벌 환경에서는 여전히 3.8.2를 사용하고 싶다면 환경 변수에서 3.8.2 경로를 맨 위로 보내준다.

bash 창을 다시 껐다 켜서 python -V를 치면 3.8.2 버전이 뜨는 것을 확인할 수 있다. 그러나 방금 만든 가상환경을 실행하면 3.6.8 버전으로 동작한다.

이와 같은 방식으로 다양한 파이썬 버전을 관리할 수 있다.

가상환경을 종료하려면 `deactivate`를 입력한다.

```bash
$ deactivate
```