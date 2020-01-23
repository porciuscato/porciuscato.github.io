---
comments: true
title: python에서 현재 설치된 패키지 목록을 모두 파일로 만드는 방법
published: 2019-11-13
updated: 2019-11-13
tags: [python, package, pip, freeze]
categories: [development]
---

현재 설치된 python 패키지를 모두 파일로 만드는 방법입니다.



#### 패키지 리스트 저장

```bash
$ pip freeze > requirement.txt
```

위 명령어로 설치된 모든 파이썬 패키지를 txt 파일로 옮깁니다.



#### 리스트에 있는 패키지 설치

```bash
$ pip install -r requirement.txt
```

위 명령어를 실행하면 리스트에 있는 모든 패키지를 한 번에 설치합니다.