---
title: youtube api
published: false
tags: [youtubeAPI]
categories: [development]
---

youtube API 사용법을 익혀서 youtube에서 원하는 정보를 가져와 봅시다.



### 1. API key 받기

youtube의 API를 사용하기 위해선 google cloud platform에서 API 키를 발급받아야 합니다. 

우선은 [사이트](https://console.cloud.google.com/)로 갑니다. 사용하기 위해선 반드시 로그인을 해야합니다. 

사이트에서 좌측 상단의 탐색 메뉴에서 `API 및 서비스` 를 선택 후 라이브러리로 들어갑니다.

<center><img src="\assets\images\etc\googleapi.jpg" width="65%"></center>

라이브러리에서 `youtube`를 검색하고 `Youtube Data API v3` 를 선택하고 `사용설정`을 클릭합니다.

<center><img src="\assets\images\etc\youtubeapisettings.jpg" width="65%"></center>

그런데 API를 사용하기 위해선 프로젝트를 생성해야 합니다.

프로젝트 생성은 아주 간단합니다. 만들기를 클릭 후 만들면 됩니다.







상태관리

데이터 변경이 일어났을 때 어떻게 관리할 것인지 고민

vuex 등을 통해 상태를 관리한다. props나 emit으로 관리하기에는 비용이 크다.