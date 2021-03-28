---
comments: true
title: WSL2에서 git 로그인 한 번만 하기
published: 2021-3-28
updated: 2021-3-28
tags: [wsl, prompt, git]
categories: [development]
---

WSL 환경은 윈도우의 git bash 환경과 다르기에 별다른 설정을 하지 않으면 remote 서버와 연동할 때마다 아이디와 비밀번호를 적어야 한다.

한 번만 로그인하도록 만들자.

1) 먼저
```bash
git config --list
```
를 적어 현재 git repo에 설정된 변수들을 확인한다.
git config --global --list는 이 시스템의 환경 설정을 볼 수 있다.

여기에 credential.helper를 추가해준다.

```bash
git config credential.helper cache
```
이후 remote 서버와 연동시 로그인을 한 번 하면 이후에는 하지 않아도 된다.

이 설정을 지우고 싶으면 다음의 명령을 입력하자.
```bash
git config --unset credential.helper
```

> 많은 변수들을 지우고 싶다면 git config --unset-all [regex] 방식을 사용하자.

\+ git config credential.helper --timeout=100000 설정을 하니 credential.helper 변수가 2개 생겼다. 지우려고 --unset 옵션을 썼지만 경고가 뜨면서 지워지지 않았다. 이때 --unset-all credential.helepr를 쓰지 모두 지워졌다.
