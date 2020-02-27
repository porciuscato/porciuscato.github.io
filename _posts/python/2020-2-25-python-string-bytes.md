---
comments: true
title: python의 strng과 bytes
published: false
updated: 2020-2-26
tags: [python, strings, bytes]
categories: [development]
---

python 의 string과 bytes에 대해 알아보자



# String

#### Unicode

&nbsp;&nbsp;유니코드는 글자를 4바이트로 표현한다. ASCII는 1바이트로서 가용 범위가 256가지 밖에 되지 않아, 전세계 모든 수를 표현할 수 없다. 2 바이트 역시 표현할 수 없다. 유니코드의 4바이트가 모두 사용되는 것은 아니지만 현존하는 모든 언어를 표현하기에는 충분하다. 유니코드의 각각 숫자는 오직 한 문자만을 가리킨다. 

&nbsp;&nbsp;하지만 이는 낭비로 보인다. 영어는 1바이트면 충분하고, 심지어 중국어도 2바이트면 모든 문자를 표현할 수 있기 때문이다. 

&nbsp;&nbsp;4 바이트를  모두 사용하는 인코딩 방식은 UTF-32(Unicode Transformation Format)라 불린다. 이는 모든 문자를 표현할 수 있지만 낭비가 심하다는 단점이 있다.

&nbsp;&nbsp;대부분의 사람들은 65535개 이상의 문자를 쓰지 않는다. 그래서 2 바이트의 유니코드 인코딩 방식도 있는데, 이를 UTF-16이라 한다. 모든 문자는 대부분 65536개를 넘지 않기 때문이다. 간혹 이 수를 넘는 경우 UTF-16은 우회적인 방법을 사용하나, 이는 극히 드문 경우다.

&nbsp;&nbsp;하지만 UTF-16에도 단점이 있다. 시스템마다 바이트를 저장하는 방식이 다르기 때문이다. 가령 U+4E2D가 UTF-16으로 저장이 된다면 빅엔디안 혹은 리틀엔디안에 따라 4E 2D, 2D 4E로 저장될 수 있다. 만약 문서들이 로컬에서만 읽힌다면 아무 문제가 없지만 네트워크로 전송이 된다면 매번 저장 방식을 알려줘야만 할 것이다. 그렇지 않다면 시스템은 두 개의 2바이트 문자를 어떻게 읽어야할 지 알 수가 없다. 이 문제를 해결하기 위해 UTF-16은 "Byte Order Mark"를 보낸다. 첫 문자열을 FFFE 혹은 FEFF로 전달하여 인코딩 방식을 알려준다.

&nbsp;&nbsp;그럼에도 UTF-16은 이상적이지 않다. 많은 문자들은 여전히 ASCII로 쓰여지며 심지어 중국 사이트 조차도 ASCII 문자가 많이 쓰인다. 이들을 모두 2 바이트 형식으로 저장하는 것은 낭비가 아닐 수 없다.

&nbsp;&nbsp;이에 대한 해답이 바로 **UTF-8**이다. UTF-8은 가변길이 인코딩 시스템이다. 즉, 다른 문자는 다른 바이트를 가진다는 뜻이다. ASCII 문자는 오직 1 바이트만 사용된다. 심지어 ASCII 코드와 완전히 같은 코드를 사용한다. 라틴어 같은 경우 2 바이트, 중국어는 3 바이트를 사용한다. 



#### Python 3

&nbsp;&nbsp;파이썬 3에서 모든 문자열은 유니코드 문자 시퀀스다. 파이썬 문자열인데 UTF-8로 인코딩 된 것은 없다. 마찬가지로 파이썬 문자열인데 CP-1252로 인코딩 된 것도 없다. UTF-8은 그저 문자를 바이트로 바꾸는 방식 중 하나일 뿐이다. 만약 문자열을 바이트로 바꾸고 싶거나, 바이트를 문자열로 바꾸고 싶다면 파이썬으로 쉽게 할 수 있다. 바이트는 문자가 아니다. 바이트는 바이트일 뿐이다. 문자는 하나의 추상이다. 문자열은 이러한 추상들의 시퀀스다.

- 문자열을 만들기 위해서는 single quotes, 혹은 double quotes를 사용한다.
- 내장함수 `len()`은 문자열의 길이를 반환한다. 이 함수는 iterable들의 길이를 구할 때도 유용하다.
- 문자열도 인덱싱으로 접근 가능하다. 그러나 리스트처럼 해당 인덱스에 재할당은 불가능하다.
- 문자열은 `+` 로 합칠 수 있다. 
- 여러 줄의 걸친 문자열은 `'''` 따옴표 3개로 여닫는다.

```python
>>> a = '學校'
>>> a_8 = a.encode('utf-8') # 6 바이트로 인코딩 된 것을 확인할 수 있다.
b'\xe5\xad\xb8\xe6\xa0\xa1'
>>> a_sig = a.encode('utf-8-sig') # 두 글자가 9 바이트로 인코딩되었다.
b'\xef\xbb\xbf\xe5\xad\xb8\xe6\xa0\xa1'
>>> type(a_8)
bytes
>>> a_8.decode('utf-8')
'學校'
```

- 값을 문자열에 넣기 위해 formatting 을 사용할 수 있다.

```python
>>> name = 'Charlse'
>>> age = '25'
>>> "{} is {} years old.".foramt(name, age)
"Charlse is 25 years old"
```

- 배열을 foramatting 할 수도 있다.

```python
>>> arr = [1,2,3,4,5,6]
>>> 'test {0[0]} and {0[1]}'.format(arr)
'test 1 and 2'
```

=> format specifiers는 파이썬 구문을 사용하는 데이터구조의 거의 모든 속성과 아이템에 접근할 수 있다. 이를 '*compound field names*'라 부른다. 리스트, 딕셔너리, 모듈, 클래스 등도 마찬가지로 사용 가능하다.

#### format specifier

- 소수점이 길 경우 원하는 만큼 자를 수 있다

```python
>>> a = 12345789,123456789
>>> '{0:.5f}'.format(a)
'123456789.12346'
```

- `0:.5f` 
  - 맨 앞의 0은 변수의 순서를 의미한다.
  - `:` 으로 숫자의 formatting을 지정할 수 있다. `.` 뒤에 오는 수는 소수점의 자릿수를 의미한다. 그 이하는 반올림한다.



### 내장함수





 'capitalize()' - 첫 글자만 대문자, 나머지는 소문자로. return, no-d
 'casefold' 
 'center(width, fillchar='')', 전체 문자열의 크기에서 가운데 정렬. width는 숫자. 전체 문자열 길이. fillchar는 빈 칸을 채울 특정 문자. return, no-d
 'count(str)', - 특정 문자 혹은 문자열이 해당하는 문자열에 몇 개나 있는지 return, no-d
 'encode(encoding, erros)' - return bytes, no-d
 'endswith(str)' - 문자열이 특정 문자열이나 문자로 끝나면 True를 반환. Tuple도 올 수 있음. 다중 옵션 가능 no-d
 'expandtabs',
 'find(str)', - 특정 문자 혹은 문자열이 처음으로 등장하는 곳의 index를 반환. 없으면 -1 no-d
 'format',
 'format_map',
 'index(str)', - 특정 문자 혹은 문자열이 처음 등장하는 곳의 index를 반환. 없으면 ValueError no-d
 'isalnum()', - 알파벳 순서로 되어있는 문자열은 True
 'isalpha', - 알파벳으로만 되어있는 문자열이면 True
 'isascii', - 아스키 코드로만 되어있으면 True
 'isdecimal', - 양의 정수로된 문자열이면 True'
 'isdigit', - 0과 1로만 구성된 문자열이면 True
 'isidentifier', - 
 'islower()', - 소문자로만 구성되어있으면 True
 'isnumeric',
 'isprintable',
 'isspace',
 'istitle',
 'isupper',
 'join',
 'ljust',
 'lower',
 'lstrip',
 'maketrans',
 'partition',
 'replace',
 'rfind',
 'rindex',
 'rjust',
 'rpartition',
 'rsplit',
 'rstrip',
 'split',
 'splitlines',
 'startswith',
 'strip',
 'swapcase',
 'title',
 'translate',
 'upper',
 'zfill'


 |
 |  casefold(self, /)
 |      Return a version of the string suitable for caseless comparisons.
 |
 |  expandtabs(self, /, tabsize=8)
 |      Return a copy where all tab characters are expanded using spaces.
 |
 |      If tabsize is not given, a tab size of 8 characters is assumed.
 |
 |
 |  format_map(...)
 |      S.format_map(mapping) -> str
 |
 |      Return a formatted version of S, using substitutions from mapping.
 |      The substitutions are identified by braces ('{' and '}').
 |
 |  isidentifier(self, /)
 |      Return True if the string is a valid Python identifier, False otherwise.
 |
 |      Use keyword.iskeyword() to test for reserved identifiers such as "def" and
 |      "class".
 |
 |  islower(self, /)
 |      Return True if the string is a lowercase string, False otherwise.
 |
 |      A string is lowercase if all cased characters in the string are lowercase and
 |      there is at least one cased character in the string.
 |
 |  isnumeric(self, /)
 |      Return True if the string is a numeric string, False otherwise.
 |
 |      A string is numeric if all characters in the string are numeric and there is at
 |      least one character in the string.
 |
 |  isprintable(self, /)
 |      Return True if the string is printable, False otherwise.
 |
 |      A string is printable if all of its characters are considered printable in
 |      repr() or if it is empty.
 |
 |  isspace(self, /)
 |      Return True if the string is a whitespace string, False otherwise.
 |
 |      A string is whitespace if all characters in the string are whitespace and there
 |      is at least one character in the string.
 |
 |  istitle(self, /)
 |      Return True if the string is a title-cased string, False otherwise.
 |
 |      In a title-cased string, upper- and title-case characters may only
 |      follow uncased characters and lowercase characters only cased ones.
 |
 |  isupper(self, /)
 |      Return True if the string is an uppercase string, False otherwise.
 |
 |      A string is uppercase if all cased characters in the string are uppercase and
 |      there is at least one cased character in the string.
 |
 |  join(self, iterable, /)
 |      Concatenate any number of strings.
 |
 |      The string whose method is called is inserted in between each given string.
 |      The result is returned as a new string.
 |
 |      Example: '.'.join(['ab', 'pq', 'rs']) -> 'ab.pq.rs'
 |
 |  ljust(self, width, fillchar=' ', /)
 |      Return a left-justified string of length width.
 |
 |      Padding is done using the specified fill character (default is a space).
 |
 |  lower(self, /)
 |      Return a copy of the string converted to lowercase.
 |
 |  lstrip(self, chars=None, /)
 |      Return a copy of the string with leading whitespace removed.
 |
 |      If chars is given and not None, remove characters in chars instead.
 |
 |  partition(self, sep, /)
 |      Partition the string into three parts using the given separator.
 |
 |      This will search for the separator in the string.  If the separator is found,
 |      returns a 3-tuple containing the part before the separator, the separator
 |      itself, and the part after it.
 |
 |      If the separator is not found, returns a 3-tuple containing the original string
 |      and two empty strings.
 |
 |  replace(self, old, new, count=-1, /)
 |      Return a copy with all occurrences of substring old replaced by new.
 |
 |        count
 |          Maximum number of occurrences to replace.
 |          -1 (the default value) means replace all occurrences.
 |
 |      If the optional argument count is given, only the first count occurrences are
 |      replaced.
 |
 |  rfind(...)
 |      S.rfind(sub[, start[, end]]) -> int
 |
 |      Return the highest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |
 |      Return -1 on failure.
 |
 |  rindex(...)
 |      S.rindex(sub[, start[, end]]) -> int
 |
 |      Return the highest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |
 |      Raises ValueError when the substring is not found.
 |
 |  rjust(self, width, fillchar=' ', /)
 |      Return a right-justified string of length width.
 |
 |      Padding is done using the specified fill character (default is a space).
 |
 |  rpartition(self, sep, /)
 |      Partition the string into three parts using the given separator.
 |
 |      This will search for the separator in the string, starting at the end. If
 |      the separator is found, returns a 3-tuple containing the part before the
 |      separator, the separator itself, and the part after it.
 |
 |      If the separator is not found, returns a 3-tuple containing two empty strings
 |      and the original string.
 |
 |  rsplit(self, /, sep=None, maxsplit=-1)
 |      Return a list of the words in the string, using sep as the delimiter string.
 |
 |        sep
 |          The delimiter according which to split the string.
 |          None (the default value) means split according to any whitespace,
 |          and discard empty strings from the result.
 |        maxsplit
 |          Maximum number of splits to do.
 |          -1 (the default value) means no limit.
 |
 |      Splits are done starting at the end of the string and working to the front.
 |
 |  rstrip(self, chars=None, /)
 |      Return a copy of the string with trailing whitespace removed.
 |
 |      If chars is given and not None, remove characters in chars instead.
 |
 |  split(self, /, sep=None, maxsplit=-1)
 |      Return a list of the words in the string, using sep as the delimiter string.
 |
 |      sep
 |        The delimiter according which to split the string.
 |        None (the default value) means split according to any whitespace,
 |        and discard empty strings from the result.
 |      maxsplit
 |        Maximum number of splits to do.
 |        -1 (the default value) means no limit.
 |
 |  splitlines(self, /, keepends=False)
 |      Return a list of the lines in the string, breaking at line boundaries.
 |
 |      Line breaks are not included in the resulting list unless keepends is given and
 |      true.
 |
 |  startswith(...)
 |      S.startswith(prefix[, start[, end]]) -> bool
 |
 |      Return True if S starts with the specified prefix, False otherwise.
 |      With optional start, test S beginning at that position.
 |      With optional end, stop comparing S at that position.
 |      prefix can also be a tuple of strings to try.
 |
 |  strip(self, chars=None, /)
 |      Return a copy of the string with leading and trailing whitespace remove.
 |
 |      If chars is given and not None, remove characters in chars instead.
 |
 |  swapcase(self, /)
 |      Convert uppercase characters to lowercase and lowercase characters to uppercase.
 |
 |  title(self, /)
 |      Return a version of the string where each word is titlecased.
 |
 |      More specifically, words start with uppercased characters and all remaining
 |      cased characters have lower case.
 |
 |  translate(self, table, /)
 |      Replace each character in the string using the given translation table.
 |
 |        table
 |          Translation table, which must be a mapping of Unicode ordinals to
 |          Unicode ordinals, strings, or None.
 |
 |      The table must implement lookup/indexing via __getitem__, for instance a
 |      dictionary or list.  If this operation raises LookupError, the character is
 |      left untouched.  Characters mapped to None are deleted.
 |
 |  upper(self, /)
 |      Return a copy of the string converted to uppercase.
 |
 |  zfill(self, width, /)
 |      Pad a numeric string with zeros on the left, to fill a field of the given width.
 |
 |      The string is never truncated.







#### 참고

- [dive into](https://diveinto.org/python3/strings.html)

