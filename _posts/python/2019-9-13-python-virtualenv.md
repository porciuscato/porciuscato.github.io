---
comments: true
title: python에서 virtual env 가상환경 사용하기
published: 2019-9-13
updated: 2019-9-13
tags: [python, virtualenv]
categories: [development]
---

파이썬에서 가상환경을 세팅하여 사용해 봅시다.



### virtualenv

1) virtualenv 패키지를 다운 받습니다.

```bash
$ pip install virtualenv
```



\+ 가상환경으로 만들 디렉터리로 들어가 아래의 명령어를 실행합니다.

2) virtualenv를 실행합니다.

```bash
$ virtualenv { 가상환경 이름 }
```

\+ 이후 가상환경 이름으로 폴더가 생성됩니다. `venv`라 해봅시다.



3) 가상환경 실행

```bash
# 윈도우 버전
$ source venv/Scripts/activate
# 리눅스 버전
$ source venv/bin/activate
```

\+ 위 명령어를 입력하면 가상환경이 실행됩니다.

\+ 이때 `pip install` 명령어를 실행하면 global 환경에서 설치되는 것이 아니라, 현재 가상환경에서만 설치가 됩니다. 

\+ bash 창에 임의의 명령어를 쳤을 때 하단에 `(venv)` 가 보인다면 실행이 되었다는 뜻입니다. 이때 venv는 처음에 실행한 가상환경 이름입니다.



4) 가상환경 종료

```bash
$ deactivate
```

