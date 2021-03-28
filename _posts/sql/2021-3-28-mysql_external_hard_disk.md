---
comments: true
title: mysql 외장하드에 데이터 저장
published: true
updated: 2021-3-28
tags: [mysql]
categories: [development]
---

mysql을 설치했으나 DB 용량의 부족으로 데이터만 외장하드에 넣으려고 한다.
잘 정리된 블로그 글이 있어서 적는다.
> 이전에 사용하던 DB는 mariaDB였는데 mariaDB는 mysql 기반으로 만들어졌음에도 이 글의 방법대로는 데이터를 외장하드에 옮길 수 없다. 그래서 mysql을 설치하여 진행했다.

[링크](https://suzxc2468.tistory.com/147)

핵심은 
1) mysql 프로세스를 종료할 것
2) mysql의 Data 폴더와 my.ini 파일을 원하는 하드디스크 폴더에 복사할 것 (이때 만약을 위해 원본을 항상 백업하자)
3) 복사한 위치에서 my.ini의 datadir 변수값을 현재 위치로 바꿀 것
4) 레지스트리에서 mysql imagepath의 datadir를 수정할 것
5) mysql을 재실행할 것
