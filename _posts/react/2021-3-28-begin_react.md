---
comments: true
title: React 시작하기
published: 2021-3-28
updated: 2021-3-28
tags: [javascript, react]
categories: [development]
---

React 시작하기

## 환경설정

node.js, npm, yarn, git, vscode를 설치하면 된다.

> yarn 혹은 chocolatey를 사용할 때 git bash창에서는 오류가 날 수 있으니, windows cmd 창을 이용하자.

## 프로젝트 생성
```bash
yarn create react-app <app name>
```

위 명령어로 리액트 앱을 생성할 수 있다. 이때 app name에 대문자는 넣을 수 없다.


yarn 앱을 생성하면 출력되는 기본 명령어들

```bash
  yarn start
    Starts the development server.

  yarn build
    Bundles the app into static files for production.

  yarn test
    Starts the test runner.

  yarn eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd page
  yarn start
```

>  \+ yarn을 사용하지 않으면 npm으로 프로젝트를 생성할 수 있다.
>
> ```bash
> npm init react-app <name>
> ```
>
> 다음 명령어로 서버를 실행할 수 있다.
>
> ```bash
> npm start
> ```



## 리액트 공식 사이트

리액트 공식 문서: https://reactjs.org/

리액트 배포 : https://cra.link/deployment