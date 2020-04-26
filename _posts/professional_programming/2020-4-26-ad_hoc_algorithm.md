---
comments: true
title: Ad hoc Algorithm
published: 2020-4-25
updated: 2020-4-25
tags: [computer science]
categories: [computer science]
---

Ad hoc algorithm 강의



# Ad hoc algorithm 학습 목표

- Ad hoc algorithm은 지식보다는 아이디어가 중요한 문제들
- 아이디어가 떠오르지 않으면 풀지 못할 수 있어서 복불복인 경향이 있음
- 하지만 아이디어가 완전히 새로운 것은 아니어서 경험이 많으면 떠오를 가능성이 높아짐
- 해결했을 때의 만족도가 매우 높음
- 가끔 현실에 등장해서 아이디어의 중요성을 보여줌





# 목차

- Anagram 찾기
- 정렬된 두 배열에서 특정한 합을 만드는 두 수 찾기
- 정렬된 두 배열을 merge 했을 때 K 번째 값 찾기
- GAP 문제
- 달리기
- 연결 리스트에서 cycle 찾기
- 혼자인 값 찾기
- Bit Manipulation 알고리즘들
- 최대 subarray 찾기
- Game [IOI 2014]



## Anagram 찾기

- 두 단어가 같은 글자들로 구성되어 순서가 다른 경우

  ex) wolf/flow

- 문제: n 개의 단어가 주어져 있고, 단어들의 길이의 합은 W이다. 단어들 중에 anagram이 되는 쌍이 있는가? 혹은, anagram이 되는 쌍의 개수를 계산하라.

  ex) flow, anagram, worf, nameless, manager, elsemans

- O(W) 시간에 찾을 수 있는가?

### First, a simpler problem

- 길이가 x, y인 두 단어가 주어졌을 때 anagram인지 확인할 수 있는가?
  - 이 문제를 빨리, 예를 들어 O(x + y) 시간에 풀 수 있으면 전체 문제에 대해 $O(n^2)$  번의 비교를 하는 방법으로 $O(Wn)$ 시간이 간단히 가능
  - 왜 $O(Wn)$? $O(Wn^2)$ 이 아닌지?
    - 길이 $x_i$인 각 단어는 $O(n)$ 번의 비교에 참여
    - 즉, 각 단어 때문에 필요한 시간은 $O(x_in)$
    - 단어들의 길이가 $x_1, x_2, x_3 .... x_n$ 이라 하고
    - 모든 단어에 대해 더하면 $O(x_1n + x_2n .... + x_nn) = O(Wn)$
- So, can you do $O(x+y)$?

  - Sort the letters and compare!
  - Anagram이면 sort한 결과가 같아야 함
  - 왜 $O(x+y)$? $O(xlogx + ylogy)$ 아닌지? -> 다음에..



- The Algorithm

  - 1. 각 단어의 letter들을 정렬 -> A

    2. 정렬된 단어들을 정렬 -> B

    3. 정렬 결과에서 인접한 단어들이 같은지 비교

       -> Anagram이 있는지 찾을 수 있고, anagram 쌍의 개수도 셀 수 있음(세는 것은 어떻게? -> 조합)

  - A. Counting sort!

    - 26 가지 letter 밖에 없음
    - 한 단어를 읽으며 각 letter가 등장하는 횟수를 셈
    - Letter count가 저장된 배열 완성
    - Letter Count를 이용하여 a부터 각 letter가 등장하는 횟수만큼 출력

  - B. Radix Sort!

    - Sort by first letter, Then, sort by second letter (recursively, within groups with same first letter) and so on...
    - 문자열을 이동하는 것은 상수 시간에 가능하다고 가정함(포인터 사용)

- 약간 코딩이 쉬운 방법

  - W+26nlogn에 비례하는 시간을 사용
    - O() notation으로는 같지만
    - W가 nlogn보다 많이 크면 이 방법이 더 빠름
    - W가 nlogn보다 많이 크지 않을 때도 훨씬 느리지는 않음
    - 이전 방법은 W + W 정도의 시간
  - 방법: B에서 문자열들을 sort하는 대신, A의 counting sort 중간과정인 26개 짜리 letter count 배열들을 sort
    - 두 문자열이 anagram 관계이면 두 문자열에 해당하는 26개 짜리 letter count 배열이 똑같아야 함
    - 이후 과정은 사실상 동일!



## 정렬된 두 배열에서 합 찾기

- 문제: 각각 크기 n인 자연수들이 정렬되어 저장된 두 배열 A, B가 주어지고 목표값 X가 주어졌을 때 두 배열에서 각각 하나의 자연수를 골라 더해서 X를 만들 수 있는가?

  ```python
  a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
  b = [11, 12, 13, 14, 15, 16, 17, 18, 19]
  ```

  - 단 같은 값은 어디에도 없는 것으로 하자.
  - 그런 경우가 있다면 한 케이스만 출력하거나, 모든 케이스들은 다 출력하는 것을 요구할 수 있다. 지금은, 한 케이스만 출력하면 된다고 하자.

- $O(n^2)$ 알고리즘은 명백

- $O(n)$ 시간 알고리즘이 있는가?

  - 주의, 모든 경우를 출력해야 하고, 입력에 같은 값이 있는 경우는 $O(n)$ 시간이 불가능



### The Slider

- 알고리즘
  - 위쪽 배열은 왼쪽, 아래 배열은 오른쪽 끝에서 시작
  - 현재 위치의 합이 목표보다 작으면 위쪽 배열의 위치를 오른쪽으로
  - 현재 위치의 합이 목표바다 크면 아래쪽 배열의 위치를 왼쪽으로
  - 반복

#### 직관도 좋지만 증명이 더 좋다.

- 혹시 빠뜨리는 경우는 없는가?
  - $N^2$개의 모든 가능한 경우를 다 검사하는 것은 아니므로
- 빠뜨리는 경우가 없다는 것을 어떻게 확인할 것인가? 
  - 빠뜨리는 경우가 있다면 반드시 일어나야 하는 상황을 도출하고
  - 그 상황이 불가능함을 보임
- 증명(**답이 있는데 빠뜨렸다고 가정**)
  - A[s] + B[t] = X가 유일한 답이라고 하고, 이 답을 못찾았다면
  - 답을 못찾았으면서 i = s, j < t인 상황이 발생해야 함
  - 그 상황 이전에 i = s, j >= t인 상황이 없었어야 함
    - 있었다면 반드시 답을 찾게 됨
  - 즉, i < s, j = t 인 상황에서 j를 감소시키는 경우가 발생해야 함
  - 이것은 당연히 불가능