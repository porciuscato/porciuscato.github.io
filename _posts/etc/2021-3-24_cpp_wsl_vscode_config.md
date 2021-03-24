---
comments: true
title: WSL로 vscode를 사용할 때 CPP 환경 설정하는 방법
published: 2021-3-24
updated: 2021-3-24
tags: [c, c++, vscode, wsl]
categories: [development]
---



윈도우즈 환경에서 WSL을 설치하고 vscode를 활용해 개발을 하자. 



## 개발환경 세팅

윈도우즈에서 C 개발을 할 때 주로 visual studio를 사용하는데, 프로젝트 단위로 파일들을 묶다보니 작은 단위의 코드를 작성해 테스트하기에는 불편하다. 그래서 직접 커맨드 라인에서 파일 단위로 컴파일을 실행할 수 있는데 이 방법에 대해 알아보자.

### WSL 설치

먼저 WSL을 설치하고 WSL2로 업데이트하자. [:link:](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

### vscode Remote - WSL 설치

이후 vscode의 확장팩 중 Remote - WSL을 설치하자. 

### WSL에서 vscode 사용

WSL과 vscode 확장팩까지 설치를 하게 되면 커맨드 프롬프트에 `wsl` 을 입력하면 리눅스 서버에 접속할 수 있다. 루트 디렉토리로 가기 위해 `cd ~` 을 입력하자.

`code .` 를 입력하면 현재 위치에서 code 실행이 가능하다.

### g++ 컴파일러 설치

C 코드를 작성하면 gcc 컴파일러를 사용해야 하고, C++ 코드는 g++ 컴파일러를 사용해야 한다.  C만 개발하면 굳이 g++을 설치할 필요는 없다. 하지만 g++을 설치하면 C 코드의 컴파일이 가능할 뿐 아니라 C의 라이브러리도 사용할 수 있기 때문에 g++을 설치하는 것이 좋다.

> g++ 컴파일러는 리눅스용 컴파일러기 때문에 윈도우즈 환경에서 개발을 하기 위해선 윈도우용 컴파일러를 사용해야 한다. `tdm-gcc` 를 설치하면 리눅스에서 처럼 gcc 명령으로 컴파일이 가능하다.

```basj
sudo apt-get install g++
```

이후 작성한 C/C++ 파일이 test.cpp 라면 컴파일하기 위해 다음의 명령어를 입력하자.

```bash
g++ test.cpp
```

이처럼 아무 옵션 없이 컴파일할 파일의 경로를 입력하면 컴파일이 실행되어 바이너리 파일이 생성된다. 아무 입력값도 넣지 않았을 때는 디폴트로 `a.out` 파일이 생성된다. 이를 실행시키기 위해선 다음의 명령어를 입력해야 한다.

```bash
./a.out
```

현재 디렉터리의 a.out 파일을 실행시키겠다는 뜻이다.

만약 만들어질 파일의 이름을 특정하고 싶다면 다음과 같이 옵션을 덧붙이면 된다.

```bash
g++ -o test test.cpp
```

`-o` 옵션은 아웃풋 옵션으로서 실행 결과를 어디에 옮길지 결정할 수 있다. 이 옵션 바로 뒤에 오는 인자는 결과물 파일의 경로 및 이름이고 다음 인자는 컴파일할 파일의 경로다.

만약 스탠다드 라이브러리를 include할 때 vscode에서 linting을 못한다면 컴파일러의 경로를 수동으로 변경해줘야 한다.

이 설정을 위해 다음의 명령어를 vscode에서 입력하자.

먼저 `ctrl + shift + p`를 입력해 명령창을 띄우고 `C/C++: Edit Configurations (UI)` 를 입력하자.

그리고 Configuration name 란에 Add configuration에 컴파일러 경로를 추가하면 된다.

g++을 설치할 경우 주로 `/usr/bin/g++` 경로에 설치가 된다. 이 경로를 입력해주고 vscode를 재실행하면 linting이 작동한다.

