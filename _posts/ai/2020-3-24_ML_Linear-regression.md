---
comments: true
title: AI study - 선형 회귀
published: false
updated: 2020-3-24
tags: [AI]
categories: [development]
---

머신 러닝의 기초 선형회귀에 대해 알아보자



다음을 가정해보자

x = [1, 2, 3]

y = [3, 5, 7]

일 때 y = f(x) 라면 x=4일 때 y는 9라는 걸 알 수 있다.

컴퓨터는 y = 2x + 1이라는 식을 어떻게 알아낼 수 있는가? -> 이것이 선형 회귀

- 비용함수
  - 선형 회귀를 통해 알아낸 함수의 정확도를 측정하는 함수
  - 