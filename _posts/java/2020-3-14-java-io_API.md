---
comments: true
title: java 기초 문법. 입출력
published: false
updated: 2020-3-14
tags: [java]
categories: [development]
---

자바를 공부하자.



## 입출력 장치를 위한 인터페이스의 필요성

장치에 따라 다른 입출력 장치를 직접 쓰는 것은 어렵다. -> interface를 사용한다.

```
절차 언어 <--> 프로그램 <--> API <--> 플랫폼
```

\+ API는 주로 함수 형태다.



## 자바 플랫폼 내장 입/출력 객체와 멤버 함수

자바는 입출력을 위한 함수들이 객체에 묶여 있다. 

- System.out.write();
- System.out.print();
- System.out.println();
- System.out.printf();
- System.in.read();
- System.in.skip();
- System.in.rest();

out과 in은 Stream 객체다.



## 출력 스트림(Output Stream)을 이용한 비동기 처리

프로그램은 여러 개가 동시에 실행되다 보면 장치 하나를 두고 입출력 받는 것의 문제가 발생한다.

여러 프로그램이 동시에 모니터에 출력하려고 하면? 근데 모니터는 하나다. -> 가장 쉬운 방법은 줄 세우기: `동기화`

그런데 동기화의 문제. 줄을 세우는 동안 기다리는 프로그램들은 멈춰있다. 그래서 다른 일을 못한다.

이를 해결하는 방법이... `버퍼`를 이용하는 것

\+ 프로그램들이 직접 모니터에 출력하는 것이 아니고, 버퍼에 올려놓으면 모니터가 버퍼에 있는 내용을 하나씩 처리한다. 이를 `출력 버퍼`라 한다. 모니터가 이를 다룰 수 있도록 도와주는 것을 `실행환경`이라 한다. 대부분 운영체제가 하지만 자바는 자바 실행환경이 행한다.

자바에서는 `OutputStream`이라 한다. 

Stream은 단방향 버퍼다. 

Stream은 많은 어플리케이션들이 비동기 형식으로 일을 할 수 있도록 만든다.



##### \+ 개체(Entity)와 객체(Object)

객체는 실존하는 것, 실체. 타입을 개체라 함.

ex) 자동차라면 아반테는 개체, 실제 매장에서 구매한 차는 객체



입출력 버퍼에서는 개체가 필요없다. 실제 존재하는 객체가 필요하다.

#### 입출력 API는 입/출력 스트림 객체를 이용한다.

출력 객체는 out, 입력 객체는 in이다. 이는 자바 환경이 만들어 놓은 객체다. 

그러므로 write함수를 쓰더라도 우리는 out 객체를 사용하여 out.write() 형식으로 출력하는 것이다.



> ##### 콘솔 입/출력과 문자 코드
>
> 키보드 입력에 대해 생각해보자. 키보드의 숫자 2를 누르면 버퍼에 2가 전달될까? 그렇지 않다. 키 코드가 전달된다. 자판 위에 보이는 것은 라벨에 불과하다. 키보드에는 자판마다 식별하기 위한 코드가 있다. 출력할 때도 이 키 코드에 전달된 값을 번역하여 출력한다. -> 이 키 코드가 ASCII다.
>
> 아스키에 각국 문자를 표현하기 위해 확장된 형태가 EUC-KR, EUR-JP 등이다. 그러나 이는 같은 코드에서 서로 다른 문자가 나오는 문제가 있다.
>
> 그래서 전 세계 모든 문자를 담고 있는 형태가 Unicode다.



#### 문자를 콘솔창에 출력하기

```java
System.out.write(3)
```

이는 out 객체에 3을 담아 버퍼에 전달하는 코드다.

```java
System.out.flush();
```

버퍼를 출력하기 위한 명령어다. 그런데 이렇게 한다고 3이 출력되지는 않는다. 

우리가 전달한 3은 integer 3이 아닌 ASCII 3이 전달된 것이기 때문이다. ASCII 표에 따르면 3은 그저 End of Text를 가리키는 기호에 불과하다. 진짜 숫자 3을 출력하려면

```java
System.out.write(51);
System.out.flush();
```

이렇게 해야한다.

그렇다면 ASCII를 모두 알고 있어야 하는가? 그렇지는 않다. `''` single quotation에 값을 넣으면 값에 해당하는 코드로 변환해준다.

```java
System.out.write('3');
System.out.flush();
```

이로써 3을 출력할 수 있게 된다.

---

```java
System.out.write('A' + 0);
System.out.write('A' + 1);
System.out.write('A' + 2);
System.out.write('A' + 3);
System.out.flush();
// ABCD가 출력된다
```



## 문자열 출력

위의 방법으로 문자열을 출력하려면 write 함수를 많이 써야하고, flush까지 호출해야 한다.

이런 반복적인 일을 대신해주는 함수가 있다.

- print()
- println()
- printf()

System.out은 출력 스트림의 이름인데, 자세하게 말하자면 여러 기능을 제공하는 (write, flush, print 등등) `응용 객체의 이름`이다.

```java
System.out = new PrintStream(new OutputStream());
```

`print()` 함수를 통해서 다음처럼 사용할 수 있다.

```java
System.out.print("hello");
System.out.print(3.54);
```

> ####  주석처리
>
> \- `// one line`
>
> \- `/* multi-line*/`

그러나 위처럼 코드를 작성하면 한 줄로 출력된다.

