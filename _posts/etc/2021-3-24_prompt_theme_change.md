---
comments: true
title: prompt의 테마 변경하기
published: 2021-3-24
updated: 2021-3-24
tags: [wsl, prompt]
categories: [development]
---



## 쉘 테마

- https://cillic.tistory.com/54 참조

1. git clone --depth=1 https://github.com/Bash-it/bash-it.git

2. ~/.bash-it/install.sh 실행한다.

   - ./bash-it/install.sh
   - 이렇게 명령어를 따라 친후 bash를 입력하면 default 값으로
   - 테마의 이름을 확인한다.
   - https://github.com/Bash-it/bash-it/wiki/Themes
   - https://bash-it.readthedocs.io/en/latest/themes-list/

3. cd ~ 로 이동한후

4. ls –al 명령어를 입력하면 .bashrc라는 파일이 존재하게 됩니다.

5. .bashrc 파일내부에  bash_it 부분에서  bash_it.sh를 가리키고 있는지 확인

6. .bashrc 내부에 있다.  ⇒ ???bash-it 폴더내부에  bash_it.sh 파일 편집

   - 그곳에서 /theme 를 검색하신후
   - export BASH_IT_THEM='powerline'
   - export BASH_IT_THEM='bobby'  ⇒ 기본
   - export BASH_IT_THEM='Bakke'

7. 설정후 다시 시작

   - exec bash

   ------

   ### jupyter theme

   - pip3 install jupyterthemes
   - jt -t chesterish
   - upgrade to latest version

   > pip install --upgrade jupyterthemes

   - 재시작

   > https://github.com/dunovank/jupyter-themes

   ------

   ## 윈도우 터미널

   - https://github.com/microsoft/terminal 에서 설치 링크 있음.
   - 색상 테마 페이지 : https://atomcorp.github.io/themes/ 각종 색상 테마를 보여주는 사이트이다. 여기서 원하는 테마를 고른 뒤 아래의 Get theme 버튼을 누르면 json양식이 클립보드에 저장되며, 이걸 그대로 settings.json 파일의 "schemes"에서 추가해 주면, 색상테마가 저장되며, 프리셋에 적용할 수 있다.