---
comments: true
title: docker 공부하기
published: false
updated: 2020-3-12
tags: [docker]
categories: [development]
---

많은 기업에서 사용하고 있는 docker에 대해 공부해보자



## Docker의 간단한 역사

도커는 Pycon US 2013에서 솔로몬 하이크Solomon Hykes에 의해 처음 소개되었다. 리눅스 컨테이너의 새로운 역사라고 소개된 도커는....?



도커는 리눅스 컨테이너 기술을 사용해서, 가상화를 하지 않고 프로세스를 격리하는 것?

기존의 운영체제 안에서 프로세스를 격리시키는 기술이다?

마치 vm을 설치한 것과 비슷한 효과

vm을 쓰면 용량을 많이 먹고, 느리고.... 

도커는 어떻게 다른가? 프로세스를 격리만 할 뿐.... 가상머신의 효과는 낼 수 있지만 가상머신은 아니다. 용량도 많이 차지 않고 속도도 빠르다.

도커는 리눅스 전용. 자동 설치 스크립트, 혹은 우분투나 centos에서 하는 것도 가능



이미지와 컨테이너. 이미지는 실행 파일. 프로세스가 컨테이너 같은 개념

docker run은 컨테이너를 실행하는 것. 

옵션을 줄 때, -i -t 이미지이름+태그 /bin/bash

메인 실행 파일을 지정해줘야 한다... 컨테이너 안에 있는 걸 실행 상태로 남겨야 함?





결국 vmware에 우분투 18.04.4 를 설치하고 진행했음



#### 참고자료

\+ 기초 자료 : [도커 튜토리얼](https://www.44bits.io/ko/post/easy-deploy-with-docker)

\+ 심화 자료 : [도커 컴포즈 활용](https://www.44bits.io/ko/post/almost-perfect-development-environment-with-docker-and-docker-compose)

\+ 동영상 강의 : [생활코딩](https://opentutorials.org/course/128/8657)

\+ [이재홍](http://pyrasis.com/Docker/Docker-HOWTO)

