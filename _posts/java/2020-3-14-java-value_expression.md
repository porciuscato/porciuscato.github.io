---
comments: true
title: java 기초 문법 = 값의 종류와 표현방법
published: false
updated: 2020-3-14
tags: [java]
categories: [development]
---

자바를 공부하자.



## 자바에서의 값의 종류와 표현방법

- 정수값
  - 26 == 032 == 0x1a == 0b11010 (4 byte)
  - 26L == 0x1aL  (8 byte)

- 실수값
  - 123.4 == 1.234e2 (8 byte) 
  - 123.4f  == 1.234e2f (4 byte)
  - 123.4d (8 byte)

- 문자값
  - 'A' == '\u0065'

- 진리값
  - true | false



## 값의 형식명칭과 변환

#### 정수 형식과 변환

`종류 + 값의 형식` 이 결합되어야 형식을 나눌 수 있다.

| 종류  | 크기 byte |
| ----- | --------- |
| byte  | 1         |
| short | 2         |
| int   | 4         |
| long  | 8         |

```java
long x = 30; // 30은 int이지만 L을 적지 않더라도 Long으로 바뀐다. (묵시적 형변환)
byte x = (byte)30; // (명식적 형변환)
```

#### 실수형식
| 종류   | 크기 byte |
| ------ | --------- |
| float  | 4         |
| double | 8         |

```java
float x = 3.5;
double x = 3.5f; // 묵시적 형변환
```

#### 문자형식

char은 2 byte지만..  자세한 내용은 나중에

#### 부울형식

boolean은 1 bit



## 변수 선언 형식

`형식명칭(한정사) + 변수명`

```java
// 변수 선언
int kor;
// 변수 초기화
int eng = 3;
// 자료형이 같을 땐 한 번에 선언
int kor1, kor2, kor3
```

\+ 변수 명명규칙도 있음