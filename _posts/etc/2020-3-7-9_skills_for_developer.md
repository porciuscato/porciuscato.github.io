---
comments: true
title: 개발자가 갖춰야할 9가지 기술
published: 2020-3-7
updated: 2020-3-7
tags: [developer, lecture]
categories: [development]
---

유튜브 강의에 올라온 박종천 넥슨 부본부장님의 강연을 정리했다. 개발자가 갖춰야할 9가지 기술은 무엇인가?



게임 회사의 부본부장님의 강연이라는 점을 감안하자.

필요한 기술을 크게 3가지로 분류하자면 Hard Skills, Soft Skills, Business Skills로 나눌 수 있다.

### Hard Skills

1. **Basic Knowledge(C++, OS)**

   - 이것들은 기본적인 것이고 혼자서 공부해야 하는 것들이다.
   - 종류에는 다음과 같은 것들이 있다.
     - Mathmatics, Physics
     - Programming Language(C++, C#, Python)
     - Algorithm, Data Structure, Design Patterns
     - Graphics, Database, Networking, AI
     - Game Engines(Unity)
     - OS (Windows, Mac, iOS, Android)
     - Tools(Source control, Visual Studio)
   - SW 업계는 빠르게 변화한다. 10년 간 썼던 기술을 버려야 하는 경우도 많다. 계속 공부해야 하는 업종이다. 

2. **Understanding for product**

   - 개발자들은 스펙대로만 만드는 경향이 있다. 하지만 UI/UX를 고려한 제품이 만들어져야 한다.
   - 제품에 대한 분석력이 뛰어나야 좋은 제품을 만들 수 있다. 훌륭한 소비자가 훌륭한 제품을 만들 수 있다. 소비자 입장에서 생각하자

3. **Development Cycle**

   ```
   명세 & 분석 -> 디자인 & 모델링 -> 개발 -> 테스트 & 배포 -> 피드백 & 업데이트
   ```

   - 개발자들은 흔히 개발에만 치중하는 경향이 있다. 이들을 1의 비율로 가야 한다. 개발을 한 달 한다면 분석 역시 1달을 가야 한다. 
   - 애자일을 하려면 어떻게 하는가? 이 사이클을 빨리 돌린다.
   - 테스트도 언어 만큼 알아야 한다. \+ 구글에서 만든 [How Google Tests Software](https://github.com/lancetw/ebook-1/blob/master/09_other/How-Google-Tests-Software.pdf)
   - 열심히 앉아서 코딩만 하는 것은 위험한 일이다.

이는 1~5년 정도하다보면 갖추게 된다. 초급 개발자라면 이 정도는 할 줄 알아야 한다. 하지만 이로는 부족하다. 개발 팀장에 오르려면 더 많은 기술을 다룰 수 있어야 한다.

### Soft Skills

보통 6~10년 정도 개발한 사람들이고 중급, 고급 개발자들이다. 팀장이 되고 싶다면 이 [책](https://www.abebooks.com/9781556156502/Debugging-Development-Process-Practical-Strategies-1556156502/plp)을 꼭 읽어볼 것을 추천한다.

4. **Project Management**

   프로젝트는 제품을 만드는 그 과정 자체다. 기술 이외에도 많은 것들이 프로젝트다.

   - Why, What, How : 이 3 질문에 대해 팀원들 모두가 답할 수 있어야 한다.

   - Triple Constraints

     - Cost (Resources)
     - Time (Schedule)
     - Scope (Quality)

     프로젝트 개발은 결국 시간과 사람(개발인력)의 싸움이다. 한 가지가 모자라서 줄이게 되면 제품은 만들어지되 질이 낮아진다. 

5. **Team Management**

   - Forming : Knowledge is hidden, Trust Unknown

     - 팀이 형성된 시기. 모이기만 해서 서로에 대해 모른다.

   - Storming : Knowledge Hoarding, Distrust

     - 마찰이 발생하며 서로에 대해 알아간다.

   - Norming : Knowledge Sharing, Collaborates

     - 협력이 발생하고 서로에 대해 잘 알며 제품 개발이 가능하다.
     - 그러나 여기서 멈추면 안 된다. 더 나아가서 창조의 단계로 가야한다.

   - Performing : Knowledge Creation, Synergizes

     - 너와 내가 아는 것을 합쳐서 새로운 것을 만들어내는 단계

     - 이 단계에서 서로의 장단점과 비전에 대해 알고 있으며 자신의 타입에 대해서도 알고 있다.

       \+ 의사소통 타입: What, Why, How, What if  -  [책](https://www.amazon.com/Teach-What-You-Know-Practical/dp/0137143680)

   \+ Roles

   서로 간 역할을 명확히 해야한다. 

   역할을 크게 4가지로 나누면 Producer, Artists, Designers, Engineers가 있다. Producer는 팀원 간 의사소통을 도와 작업이 원활하게 이뤄지도록 돕는 사람이다. Artists는 UI/UX를 만드는 사람이다. Designers는 제품을 기획하는 사람이다. 

   Engineer는 무엇인가? 실패를 막는 사람이다. 사실상 제품의 성공은 기획과 UI/UX에 달려있는 것이다. 엔지니어의 역할을 기획이 에러 없이 작동하도록 만드는 것이다.

6. **Process (Agile, Zero-Bug)**

   제품, 기술, 사람 자체를 다루는 것 자체가 Process다. 

   프로세스 자체가 많은 것들을 보호해준다. 누구 하나가 실패하더라도 개발 과정에 문제가 생기지 않도록 만드는 것이 프로세스다.

   - 개발 과정의 최적화
     - Detect Failure, Prevent Failure
   - 프로젝트 관리 프로세스
     - 폭포수, 애자일/스크럼
   - 개발 프로세스
     - 개발 사이클, 코드 리뷰
     - [The Joel Test(12 steps)](https://www.joelonsoftware.com/2000/08/09/the-joel-test-12-steps-to-better-code/) : 이 중 8~9개 정도는 해야 잘하고 있는 것

   \+ PMMM : Project Management Maturity Model

   1. Initial = Common Language

      팀원들이 모두 같은 언어를 사용해야 한다. 한 용어에 대해 서로 같은 이해를 가지고 있어야 한다. 의사소통이 잘 되는 것은 굉장히 중요하다.

   2. Repeatable = Common Process

      일하는 방식이 정해져 있어야 한다. 테스트, 빌드 하는 방식 등등. 매번 프로세스가 바뀌는 것은 위험하다.

   3. Defined = Singular Methodology

      조직 전반에 걸쳐 프로세스가 일관되어 있어야 한다. 가령 다른 팀으로부터 지원을 받더라도, 동일한 프로세스와 방법론은 일이 용이하게 진행되도록 만든다.

   4. Managed = Benchmarking

      회사를 검토하고 측정하는 것

   5. Optimized = Continuous Improvement

      4번을 바탕으로 회사를 변화시키는 것

   => 1만 해도 훌륭한 회사고, 3까지 가면 성공하는 회사다. 

### Business Skills

Soft 스킬 까지 있더라도 제품 개발하는 데에는 문제가 없다. 하지만 더 높은 개발자가 되기 위해서 필요한 기술들이 있다.

이런 기술은 10년차 이상의 개발자, 리드 개발자, CTO, CEO 등에 해당한다.

7. **HR System**

   채용, 평가, 교육, 보상, 승진 등등이 인사 시스템에 해당한다.

   \+ Performance Review(개발자의 경우) : 개발자를 평가하는 7가지 기준

   - Productivity
   - Professionalism (Reliability)
   - Teamwork (Communication)
   - Knowledge
   - Functoinality (No Defect)
   - Implementation (Good Code)
   - Design & Architecture

8. **Business Management**

   - Leading People, Manage Business

   비즈니스는 끝도 없다. 

   - Capability, Strategy, Tactics, Finance, Economics, Marketing, Sales, CS, Operations. Change

9. **Vision/Goals/Culture**



비즈니스 스킬은 아직까지 너무 먼 미래처럼 보인다.

정리하면 다음과 같다.

- Hard Skills : Learn by Studying
  - Basic Knowledge
  - Understanding for product
  - Development Cycle
- Soft Skills : Learn by Experience
  - Project Management
  - Team Management
  - Process
- Business Skills : Learn from People
  - HR System
  - Business Management
  - Vision/Goals/Culture



출처 : [유튜브](https://www.youtube.com/watch?v=fHyTA-UIcqs)