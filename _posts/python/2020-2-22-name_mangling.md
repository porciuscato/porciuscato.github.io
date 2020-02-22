---
comments: true
title: name mangling이란
published: 2020-2-22
updated: 2020-2-22
tags: [python, name mangling]
categories: [development]
---

name mangling이 무엇인지 알아봅시다.



# name mangling이란?

&nbsp;&nbsp;간단하게 말하면, 컴파일러가 임의로 함수, 변수 등의 이름을 변경하는 것을 말합니다. 그러면 왜 이름을 변경해야 하는 걸까요?

&nbsp;&nbsp;이는 function overloading과 관련이 있습니다. 함수 오버로딩은 동일한 함수명의 각기 다른 작업을 가능케 합니다.

&nbsp;&nbsp;C++를 예를 들어보겠습니다.

```C++
int mul(int a, int b){return a * b;}
float mul(float a, float b){return a* b;}
float mul(float a, float b, float c){return a * b * c;}
```

&nbsp;&nbsp;위의 함수는 세 가지 방식으로 호출될 수 있습니다. int 형의 매개변수 2개를 받거나, float 형의 매개변수 2개를 받거나, 3개를 받는 형식입니다. 동일한 함수 이름 mul로 호출하게 된다면 컴파일러는 이에 맞는 함수를 어떻게 찾는 것일까요? 이것이 가능한 이유가 바로 name mangling입니다. 

&nbsp;&nbsp;컴파일러는 함수의 symbol을 만들때 함수명과 함수 매개변수를 종합하여 symbol을 만듭니다. 가령 int mul(int a, int b)를 mul + int + int -> mulinin 이런 형식으로 만든다는 것입니다(실제 컴파일러의 동작과는 무관한 필자의 예시입니다.). 이것을 name mangling이라 부릅니다.