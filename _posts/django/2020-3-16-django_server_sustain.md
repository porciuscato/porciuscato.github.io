---
comments: true
title: django 서버 콘솔창에서 유지하기
published: 202-3-16
updated: 2020-3-16
tags: [python, django, backend, restframework, swagger]
categories: [development]
---

django REST의 swagger를 사용해 봅시다.

콘솔 창을 꺼도 django 서버가 유지되도록 하는 방법이다.



### django 서버 유지

배포 서버에 django를 올리고 django를 실행시키려면 다음의 명령어를 입력해야 한다.

```bash
$ python3 manage.py runserver 0.0.0.0:8000
```

해당 IP의 8000번 포트에서 실행한다는  의미다. 주로 django를 Backend로 다루기 때문에 포트 번호 옵션을 주었다.

그런데 문제는 서버를 실행시키고 콘솔 창을 끄면 서버도 같이 꺼진다는 것이었다.

어떻게 하면 콘솔창을 끄고도 서버가 유지되도록 만들 수 있을까?



### Screen을 이용한 서버 유지

screen은 터미널을 다중화하여 사용할 수 있게 만들어 준다. 현재 콘솔창 이외에 다른 창을 띄워 서버를 실행시키면, 그 창을 닫더라도 서버가 유지된다.

사용법은 아래와 같다. 먼저 설치한다.

```bash
$ sudo apt-get update && sudo apt-get install screen
```

설치가 끝나면 screen을 생성한다. 

```bash
# django라는 이름의 스크린 하나를 생성한다.
$ screen -S django
```

생성된 screen의 종류를 확인할 수 있다.

```bash
# 현재 생성된 스크린 list를 조회한다.
$ screen -ls

There is a screen on: 
		23374.django	(03/16/2020 05:10:13 AM)	(Attached)
1 Sockets in /run/screen/S-ubuntu.
```

23374라는 아이디로 django 스크린이 생성되었다.

Attached는 현재 들어와 있는 스크린의 상태를 의미한다.

`ctrl + a + d` 를 누르면 해당 스크린에서 나온다.  

다시 screen -ls를 치면 detached가 된 것을 확인할 수 있다.

##### 서버 실행

이제 할 일은 생성한 screen으로 들어가 서버를 실행하는 것이다.

먼저 생성한 스크린으로 들어간다.

```bash
$ screen -r 23374
```

스크린에서 django를 실행한다.

```bash
$ sudo python3 manage.py runserver 0.0.0.0:8000
```

이제 서버의 IP 주소의 8000번 포트로 접속이 가능하다. 

`ctrl + a + d`를 눌러서 스크린을 빠져 나온 뒤, 콘솔 창을 끄더라도 여전히 실행중인 것을 확인할 수 있다.



#### 참고

[블로그](https://dailyheumsi.tistory.com/19)

```html
nohup python manage.py runserver 0.0.0.0:8000
```