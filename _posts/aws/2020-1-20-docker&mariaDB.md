---
title: docker 사용 기본 환경설정하기
published: false
updated: 2020-1-20
tags: [docker, aws]
categories: [development]
---

docker 사용을 위한 환경설정을 해봅시다.



## 1. Docker

  Docker는 컨테이너 기반 오픈소스 가상화 플랫폼입니다. 개발 및 운영에 필요한 여러 서버를 가상 환경에서 사용할 수 있게 해주는 프로그램입니다. 

  Docker는 DB 서버, Web 서버를 가상화시킵니다. 만약 서버 구축 중 세팅에 오류가 생긴다면 서버를 다시 설치하는 것이 아니라 컨테이너만 삭제하면 되기에 개발 환경 관리가 쉬워집니다. 

\+ [AWS의 Docker 설명](https://aws.amazon.com/ko/docker/)

\+ [왜 굳이 도커를 사용해야 하는가?](https://www.44bits.io/ko/post/why-should-i-use-docker-container)



## 2. MariaDB

  MariaDB는 MySQL과 동일한 소스 코드를 기반으로 만들어진 RDBMS입니다. 

\+ [MariaDB](https://mariadb.com/kb/ko/mariadb/)

\+ maria DB에 json 파일 넣기



## 3. Docker + MariaDB

1) 윈도우 10에서 Docker for Windows를 설치합니다.

- [사이트](https://docs.docker.com/docker-for-windows/install/)로 들어가 로그인을 하고 `Download from Docker Hub` 를 클릭합니다.

- 설치 후에 다음의 명령어를 bash 창에 입력하여 설치 여부를 확인합니다.

  ```bash
  docker -v
  ```


2) 가상화에 필요한 Hyper-V도 함께 설치합니다.

- 다음의 링크로 들어가 [설치](https://docs.microsoft.com/ko-kr/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)를 진행합니다.

3) Docker 실행 후 아래 명령어를 입력하여 MariaDB 컨테이너를 실행합니다.

```bash
docker run --name maria-db -p 3306:3306 -e MYSQL_ROOT_PASSWORD={패스워드} -d mariadb
```

4) Docker 명령어로 DB에 접속해봅니다.

```bash
docker exec -it maria-db -u root -p
```









설치시 가상화에 필요한 요소인 Hyper-V도 함께 [설치](https://docs.microsoft.com/ko-kr/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)한다.