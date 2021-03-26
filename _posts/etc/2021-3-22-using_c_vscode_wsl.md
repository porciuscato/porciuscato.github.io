---
comments: true
title: how to use c complier in wsl vscode
published: 2021-3-22
updated: 2021-3-22
tags: [c++, vscode, wsl]
categories: [development]
---



wsl 에서 c와 c++ 파일을 컴파일하고 실행하는 방법이다.

gcc, g++ 컴파일러를 사용한다.

## C 컴파일

```bash
gcc -o <executable file name> <complied file name>
```

즉 test.c 파일을 컴파일하기 위해서

```bash
gcc -o main test.c
```

이렇게 입력하면 된다.

## C++ 컴파일

c++ 파일

```bash
g++ -o main test.cpp
```

구조는 gcc와 같다.



## vcpkg 설치

standard 라이브러리를 사용하지 못할 수 있다. 이때는 아래 링크를 참조해 vcpkg를 설치하고, integrate install을 통해 모든 사용자들이 라이브러리를 사용할 수 있게 만들자.

[링크](https://docs.microsoft.com/en-us/cpp/build/vcpkg?view=msvc-160)

How to get and use vcpkg에서 [Install vcpkg](https://docs.microsoft.com/en-us/cpp/build/install-vcpkg?view=msvc-160), [Integrate vcpkg](https://docs.microsoft.com/en-us/cpp/build/integrate-vcpkg?view=msvc-160), [Manage libraries with vcpkg](https://docs.microsoft.com/en-us/cpp/build/manage-libraries-with-vcpkg?view=msvc-160) 를 따라서 vcpkg를 설치하자.

vcpkg를 git clone 한 다음, vcpkg의 root 디렉터리로 이동해 실행하자.

```
cd vcpkg
./bootstrap-vcpkg.sh
```

설치가 완료되면

```bash
./vcpkg integrate install
```

를 통해 모든 사용자들이 사용할 수 있게 만들자.