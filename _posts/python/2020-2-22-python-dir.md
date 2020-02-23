---
comments: true
title: python dir 함수로 속성, 함수, 메소드 알아내기
published: 2020-2-22
updated: 2020-2-22
tags: [python, dir]
categories: [development]
---

python dir 사용하기



### dir function

&nbsp;&nbsp; 특정 모듈이나 함수가 가진 속성과 메소드를 모두 볼 수 있는 함수로써 python3를 사용하다보면 참으로 유용한 내장함수입니다. documentation을 보지 않더라도 dir 만으로도 많은 정보를 얻을 수 있죠.

&nbsp;&nbsp;사용법은 다음과 같습니다.

```
dir({object})
```

object 부분에 확인이 필요한 모듈을 넣으면 사용할 수 있는 속성, 및 함수들이 나오게 됩니다.

가령, `[]`(List)를 넣으면 아래와 같은 결과가 나옵니다.

```python
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

&nbsp;&nbsp;`dir()`은 List를 반환 합니다. 그래서 dir()에 매개변수로 dir()을 전달하면 위처럼 리스트와 동일한 결과를 반환합니다.

```python
>>> dir(dir())
... # 위와 동일
```



#### 그냥 dir()을 print하면 어떤 일이 벌어질까요?

해당 파일에 있는 모든 name, 이름들이 출력됩니다. 이름들에는 변수명 뿐 아니라, 함수, 클래스와 임포트된 모듈들을 포함합니다.

안의 구조를 알고 싶은 모듈이 있다면 vscode 상에서는 `ctrl + 클릭`으로 해당 모듈로 직접 가서 확인할 수 있습니다. 그렇지만  dir() 안에 매개변수로 모듈을 전달하면 해달 모듈에 있는 모든 이름들이 출력되는 걸 확인할 수 있습니다.

예로, `dir(os)`를 출력하면 다음과 같은 리스트를 볼 수 있습니다.

```python
['DirEntry', 'F_OK', 'MutableMapping', 'O_APPEND', 'O_BINARY', 'O_CREAT', 'O_EXCL', 'O_NOINHERIT', 'O_RANDOM', 'O_RDONLY', 'O_RDWR', 'O_SEQUENTIAL', 'O_SHORT_LIVED', 'O_TEMPORARY', 'O_TEXT', 'O_TRUNC', 'O_WRONLY', 'P_DETACH', 'P_NOWAIT', 'P_NOWAITO', 'P_OVERLAY', 'P_WAIT', 'PathLike', 'R_OK', 'SEEK_CUR', 
'SEEK_END', 'SEEK_SET', 'TMP_MAX', 'W_OK', 'X_OK', '_Environ', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', 
'__package__', '__spec__', '_execvpe', '_exists', '_exit', '_fspath', '_get_exports_list', '_putenv', '_unsetenv', '_wrap_close', 'abc', 'abort', 'access', 'altsep', 'chdir', 'chmod', 'close', 'closerange', 'cpu_count', 'curdir', 'defpath', 'device_encoding', 'devnull', 'dup', 'dup2', 'environ', 'error', 
'execl', 'execle', 'execlp', 'execlpe', 'execv', 'execve', 'execvp', 'execvpe', 'extsep', 'fdopen', 'fsdecode', 'fsencode', 'fspath', 'fstat', 'fsync', 'ftruncate', 'get_exec_path', 'get_handle_inheritable', 'get_inheritable', 'get_terminal_size', 'getcwd', 'getcwdb', 'getenv', 'getlogin', 'getpid', 'getppid', 'isatty', 'kill', 'linesep', 'link', 'listdir', 'lseek', 'lstat', 'makedirs', 'mkdir', 'name', 'open', 'pardir', 'path', 'pathsep', 'pipe', 'popen', 'putenv', 'read', 'readlink', 'remove', 'removedirs', 'rename', 'renames', 'replace', 'rmdir', 'scandir', 'sep', 'set_handle_inheritable', 'set_inheritable', 'spawnl', 'spawnle', 'spawnv', 'spawnve', 'st', 'startfile', 'stat', 'stat_result', 'statvfs_result', 'strerror', 'supports_bytes_environ', 'supports_dir_fd', 'supports_effective_ids', 'supports_fd', 'supports_follow_symlinks', 'symlink', 'sys', 'system', 'terminal_size', 'times', 'times_result', 'truncate', 'umask', 'uname_result', 'unlink', 'urandom', 'utime', 'waitpid', 'walk', 'write']
```

모듈을 하나씩 뜯어보며 안에 무엇이 들어있는지 살피는 것은 참으로 흥미롭습니다. 생각지도 못했던 기능들을 발견하게 될 수도 있으니까요.