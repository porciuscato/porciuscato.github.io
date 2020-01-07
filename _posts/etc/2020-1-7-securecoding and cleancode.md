---
comments: true
title: Secure coding
published: false
updated: 2020-1-7
tags: [secure]
categories: [computer science]
---

secure coding이란 무엇이고 왜 필요한가



## 시큐어코딩

1. 시큐어 코딩이란?
2. 사고 사례기반 시큐어 코딩의 필요성
3. 보안취약점 진단 및 보안약점 제거



## 1. 시큐어 코딩이란?

- 안전하게 코드를 작성하는 것
  - 왜 안전하게 작성해야하는가?
    - 빠르게 코드들만을 작성하다보니 보안 문제가 발생
    - 소프트웨어의 흠결이 예전에는 단일적으로 적용이 되었다. 하지만 IoT의 발전으로 지금은 한 곳만 뚫려도 네트워크 상 연결된 모든 곳이 해킹의 위협에 내던져지게 되는 것이다.

#### Secure Software란?

- 실수를 줄이고
- 버그를 줄이고
- 장애를 줄이는 것



\+ 보안사고의 75% 이상이 애플리케이션 취약서이 원인

방화벽 0.5%

IDS/IPS 3%

웹방화벽 10%

애플리케이션 서버 75% -> 소스 코드에 문제가 있었던 것

\+ 위는 2005년 통계. 최근에는 78%까지 증가. 시큐어 코딩의 중요성을 강조하였지만 오히려 증가



## 2. 사례

1) 농협

> 사내에서 쓰던 노트북을 외부로 반출해서 영화를 다운 받고 그 노트북을 다시 사내로 들였음. 이때 웜이 침투하여 농협 전산망을 타고 문제를 일으킴

2) SK 컴즈 고객정보 유출

> 해커가 알약서버에 악성코드를 유포. 컴즈가 그대로 알약을 다운받아 사용. 컴즈의 고객정보가 대거 유출 됨

3) KT 개인정보 유출

> 웹 파라미터를 변경하여 고객들의 정보를 유출. 파라미터와 요청자가 동일한 인물인지 확인하는 코드가 없었기 때문에 발생



### 최신 정보보호

\+ 정보보호 트렌드

마이크로칩, CPU, 인공지능 삼성 검색하면...

AI가 적용된 칩셋을 만들 예정

AI를 모르면 도퇴되는 상황 -> 강추가 AI + 가상화(가상 네트워크도 수급난이 있음)



#### 랜섬웨어

운영체제나 시스템에 락을 걸어버리는 것. 

물리적으로 아예 다른 서버에 백업본을 둘 것

#### 크립토재킹

남의 자원을 사용하여 암호화폐를 채굴하게 만든 것(자바스크립트로 구현되었기 때문에 웹브라우저가 있는 곳에 코드를 심어서 채굴을 함)

#### 오버플로우와 언더플로우 취약점을 이용한 코인 탈취



#### SW 보안약점, SW 보안취약점

소프트웨어는 보안 약점을 가질 수 밖에 없다. 보안 취약점은 보안 약점 중 공격으로 이어질 수 있는 부분.



### CVE

http://cve.mitre.org

-> CVE + 년도 + 일련번호



SANS TOP 25 Most Dangerous Software Errors



OWASP TOP

등에서 보안 문제 랭킹을 선정



#### SQL 인젝션 취약점으로 인한 개인정보 유출사고

#### SQL 인젝션

- 500 에러가 뜨면 이를 토대로 서버의 정보를 알 수 있음

or 1=1

or 연산자 덕분에 전체 연산을 참으로 만들어 줌 => 모든 결과를 참으로 만들어줌

Mysql은 #이 인라인 주석이기 때문에  `'' or 1=1` 로 만들면 

인증우회기법

아이디 뒤에 `'\` 넣어서 쿼리문을 무효화 만들어버린다.

#### union 인젝션

select union select





[wayback machine](https://web.archive.org/) 사이트

해커들이 어떤 정보를 활용할까

-> 사이트의 과거 페이지로 들어가서 공격을 하는 것이 훨씬 용이할 수 있다. 과거 페이지의 링크가 아직도 DB와 유효하게 연결되어 있다면 현재에도 서버와 연결이 되어있다는 것. 현재 페이지는 공격하기 어려우니 과거의 기록을 통해 접근하는 방식



[shodan](https://www.shodan.io/)

 K대 보안 취약



#### 크로스사이트 스크립트(XSS)





kali linux

공격용?



beef

ddos 공격에 많이 쓰였던 툴



스프링을 사용하면 들어오는 데이터를 모두 검증할 수 있음

자바스크립트를 사용자에게 보내서 상대 브라우저에서 작동하게 만드는 방법

-> 자바스크립트 언어로 쓰일 만한 것들을 모두 필터링 시켜야 한다.





#### 잘못된 기능 접근 제어

관리자페이지, 특정사용자만이 들어가야 하는 페이지

위변조할 수 있는 방법은 서버로 넘어가는 변수들을 건드리는 것

-> 사용자에게 받은 데이터는 절대 쓰면 안 된다. 세션 정보 등 신뢰할 수 있는 정보를 활용해야 한다.



#### 파일 업로드/다운로드 취약점

웹 쉘을 통해 사이트를 뒤질 수 있다.

jsp 파일 등을 올리면 쉘을 볼 수 있게 될 수도...

업로드의 경우 취약점 발생 원인

- 파일의 타입을 제한하지 않는 경우
- 파일의 크기나 갯수 제한제하지 않는 경우
- 업로드된 파일을 외부에서 직접적으로 접근가능한 경우
- 업로드된 파일의 이름과 저장된 파일의 이름이 동일하여 공격자가 파일에 대한 인식이 가능한 경우
- 업로드 된 파일이 실행권한이 있는 경우

다운로드의 경우 취약점 발생 원인

- `.. /` 같은 것들이 들어올 수 없도록 만드는 것이 중요





\+ 소프트웨어 개발보안 가이드 (행안부 문서)



---

## 클린 코드

#### 1. 클린 코드

대가들이 생각하는 클린 코드는?

- 코드가 문장처럼 읽힌다.
- 한 번에 하나의 제어만

=> 팀원들이 이해하기 쉽도록 짜라

나쁜 코드는?

- 르블랑의 법칙 : Later equals never



#### 클린코드의 주요원칙

- follow standard convention : 표준을 따라라
- keep it simple, stupid : 단순하게 하라
- boy scout rule : 수정하더라도 과거보다 더 깨끗해야 한다.
- root cause analysis : 근본원인을 찾아라(미봉책 말고)
- do not multiple language in one source file



\+ 클린코드의 주요원칙(class design)

: SOLID

[Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)[[6\]](https://en.wikipedia.org/wiki/SOLID#cite_note-6)

A [class](https://en.wikipedia.org/wiki/Class_(computer_programming)) should only have a single responsibility, that is, only changes to one part of the software's specification should be able to affect the specification of the class.

[Open–closed principle](https://en.wikipedia.org/wiki/Open–closed_principle)[[7\]](https://en.wikipedia.org/wiki/SOLID#cite_note-7)

"Software entities ... should be open for extension, but closed for modification."

[Liskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)

"Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program."

[Interface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle)[[9\]](https://en.wikipedia.org/wiki/SOLID#cite_note-9)

"Many client-specific interfaces are better than one general-purpose interface."

[Dependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)

One should "depend upon abstractions, [not] concretions."



\+ 코드리뷰가 있는 회사에 들어가면 개발자로서 실력을 쌓는데 도움이 된다.



#### 코드 리뷰시 무엇을 확인해야 하는가?

- 기능의 정상 동작 여부
- 버그의 조기 발견
- 가독성과 유지보수 편의성
- 개발표준의 준수 여부
- 테스트 코드의 작성 여부: 테스트 코드가 없으면 무엇을 기준으로 잘 동작하는지 확인할 수 있는 길이 없음
- 재사용 가능한 모듈의 중복 개발
- 배울만한 점은 없는지



#### 코드리뷰에서 주의해야할 점들

- 코드의 맥락을 이해할 수 있는 설명을 추가하라
- 하나의 이슈 당 하나의 코드 리뷰
- 리뷰 받는 코드는 한 번에 500 줄 이하



\+ pull panda. 코드 리뷰 요청을 계속 보내주는 





#### 리팩토링

겉으로 보이는 동작은 같지만 내부 구현을 바꾸는 것

++ [설명](https://sourcemaking.com/refactoring)



깨끗한 코드 -> 문장처럼 읽힌다.

의미있는 이름 -> 의도를 드러내라

함수와 주석 -> 프로그래밍은 글짓기

