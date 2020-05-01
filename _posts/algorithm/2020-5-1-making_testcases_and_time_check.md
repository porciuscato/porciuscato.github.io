---
title: python 으로 알고리즘 문제 테스트 케이스 만들기 & 코드 실행시간 확인하기
published: false
updated: 2020-5-1
tags: [python, testcase, algorithm]
categories: [development]
---

python 으로 알고리즘 문제 테스트 케이스 만들기 & 코드 실행시간 확인하기



## 테스트케이스 만들기

삼성 코딩 테스트의 테스트 케이스를 만드는 방법이다.

1. Python

   ```python
   import sys
   import random
   # print 결과를 텍스트로 출력한다.
   sys.stdout = open("input.txt", "w")
   
   N = 8
   # N * N 크기의 2차원 배열 모양으로 테스트 케이스를 생성한다.
   arr = [[0] * N for i in range(N)]
   
   print(N, N)
   for i in range(N):
       for j in range(N):
           t = random.randint(0, 2)
           if t == 2 and (i * j) % 10:
               t = 0
           elif t == 1 and (i * j) % 5:
               t = 0
           # 같은 줄에 있는 것들을 출력하기 위해 end=' ' 옵션을 주었다.
           print(t, end=' ')
       # 줄바꿈
       print()
   ```

2. CPP

   ```cpp
   #define _CRT_SECURE_NO_WARNINGS
   #include <iostream>
   #include <cstdlib>
   #include <ctime>
   using namespace std;
   
   void testcase() {
       // seed 생성
   	srand(unsigned int(time(NULL)));
   	freopen("input.txt", "w", stdout);
   	int scope = 100;
   	int T = 10;
   	cout << T << "\n";
   	for (int i = 0; i < T; i++) {
   		cout << scope << "\n";
   		for (int s = 0; s < scope; s++) {
   			cout << rand() % 10 + 1 << " ";
   		}
   		cout << "\n";
   	}
   }
   
   int main() {
       ios::sync_with_stdio(false);
   	cin.tie(0);
       
   	testcase();
   }	
   ```

   



## 실행시간 확인하기

실행시간을 확인하는 방법이다.

1.  Python

   - 하나

     ```python
     import time
     # 코드 시작시 시간을 기록
     start = time.time() 
     '''
     코드 진행
     '''
     # 종료 시간에서 시작 시간을 뺌
     print(time.time() - start) 
     ```

   - 둘

     ```python
     from datetime import datetime
     start = datetime.now()
     '''
     코드 진행
     '''
     print(dtetime.now() - start)
     ```



2. CPP

   - 하나

     ```cpp
     #include <iostream>
     #include <ctime>
     using namespace std;
     int main() {
     	clock_t start = clock();
     	// 코드 실행
         // clock_t 를 int나 double로 바꿔도 상관 없음
     	cout << clock_t(clock() - start) << " ms";
     }
     ```

     