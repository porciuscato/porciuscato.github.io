---
comments: true
title: vscode에서 python 경로와 pylint 경로를 설정하는 방법
published: 2021-4-17
updated: 2021-4-17
tags: [python, vscode]
categories: [development]
---



python  개발은 workspace 내 virtualenv를 구성하는 방식으로 이루어진다.

하지만 vscode 에서 코드를 작성하고 실행시키면 세팅한 가상환경의 파일이 실행되지 않고 글로벌 환경에서 실행되는 것을 볼 수 있다.

이는 python 경로가 설정되지 않았기 때문인데 경로를 setting에서 바꾸면 문제가 해결된다.

## python 경로 바꾸기

`F1`  을 누르면 모든 커맨드를 검색할 수 있다. 이때 `python: select interpreter`  를 검색하자.

그러면 설정가능한 python 경로들이 보이는데, 여기에도 venv 파일의 python.exe 파일이 보이지 않는다면 최상단의 `Enter interpreter path` 를 선택해 직접 경로를 추가하자.

` find`를 눌러 `python.exe` 의 경로를 추가하면 된다.

윈도우즈 기준으로 기본 경로는 `venv/Scripts/python.exe`다. 이 경로를 선택하자.

이후  python 파일이 실행되면 경로가 제대로 되는 것을 확인할 수 있다.



## pylint의 경로 바꾸기

우선 `pylint`도 라이브러리기 때문에 새로 생성한 virtualenv 에 pylint 가 없다면 설치해야한다. 

```bash
pip install pylint
```

그리고 pylint 를 linter 경로에 추가해주면 된다.

`f1`을 누르고 `Preference: Open Workspace Settings` 을 입력한 다음 python 세팅 중 `Python > Linting: Pyling Path` 를 선택해 경로를 추가하면 된다. 

```
venv\Lib\pylint
```



## settings.json 파일 수정하기

혹은 settings.json 파일에서 수정하면 된다.

workspace 단위로 생성되는 .vscode 파일의 settings.json 을 통해 작업 단위로 세팅이 가능하다.

```json
{
    "python.pythonPath": "venv\\Scripts\\python.exe",  // python interpreter의 경로
    "python.linting.pylintEnabled": true,  // pylint 사용 여부
    "python.linting.enabled": true,
    "python.linting.pylintPath": "venv\\Lib\\pylint",  // pylint의 경로
}
```

 이처럼  settings.json 파일을 직접 수정해 설정을 변경할 수도 있다.