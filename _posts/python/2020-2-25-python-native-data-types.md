---
comments: true
title: python native data types
published: 2020-2-25
updated: 2020-2-25
tags: [python]
categories: [development]
---

python 의 native data types에는 무엇이 있는가?



# Data types

파이썬은 다른 언어와는 달리 데이터 타입을 선언할 필요가 없다. 파이썬은 인터프리터가 런타임에 자료형을 검사하기 때문이다. 

> ### 참고: 파이썬 자료형의 특징
>
> - `동적 검사` : 런타임에 변수의 자료형을 검사한다.
> - `동적 타이핑` : 특정 자료형으로 정의된 변수에 다른 자료형의 값을 할당할 수 있다.
> - `타입 추론` 또는 `암시적 타입 선언` : 인터프리터가 자료형을 추론하여 알맞은 타입을 추론한다.
> - `강타입` 언어 : 암시적 형변환을 지원하지 않아 런타임에 타입 오류를 만나면 에러가 발생한다.
>
> \+ [출처](https://planbs.tistory.com/entry/Python-%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%9D%98-%ED%83%80%EC%9E%85-%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B3%BC-%ED%83%80%EC%9E%85-%EB%B3%80%EC%88%98-%EC%84%A0%EC%96%B8%EA%B3%BC-%EC%9E%AC%EC%A0%95%EC%9D%98)



파이썬에서 모든 값은 데이터타입을 가지고 있다. 내장함수 `type()` 을 사용하면 타입을 확인할 수 있다. 다양한 native data type 들이 있는데, 그 중 아래의 타입들이 중요하다.

1. **Booleans** 

   - True , False 값을 가진다.

2. **Numbers**

   - int, float, fractions, complex 를 포함.

3. **Strings**

   - 유니코드 문자들의 연속체.

4. **Bytes** and **byte arrays**

   ​	ex) JPEG 이미지 파일 등등

5. **Lists**

   - 순서가 있는 값들의 연속체(ordered sequences of values).

6. **Tuples**

   - 순서가 있지만 변경이 불가능한 값들의 연속체(ordered, immutable sequences of values).

7. **Sets**

   - 순서와 중복이 없는 값들의 집합.

8. **Dictionaries**

   - key-value pairs

파이썬의 모든 변수는 객체다. 그래서 모듈, 함수, 클래스, 메소드, 파일, 컴파일 코드 등도 모두 데이터 타입이 될 수 있다. 하지만 위의 8가지가 가장 기본이 되는 데이터 타입들이다.

> \* 모든 변수는 객체이기에 **`dir()`** 함수를 사용하면 해당 객체가 가진 속성과 메소드를 확인할 수 있다.



## 1. Booleans

- 비교 연산자의 결과는 항상 True or False다.

  ex) 1 < 0, 1 >= 0 등등

- True는 1, False는 0이다. 

  - True + True는 2지만 이런 식은 사용하지 말자.

- 숫자는 0을 제외한 모든 수가 True다.

- Iterable은 비어있는 경우를 제외하고 모두 True다.

- String은 빈 리스트를 제외하고 모두 True다.



## 2. Numbers

- `type()` 함수를 통해 확인할 수 있다. 
- `isinstance(var, type)` 함수로 해당 변수가 특정 타입인지 파악할 수 있다.
- int와 int를 더하면 int지만, int와 float을 더하면 float이다.

- `float()` 함수로 int를 float으로 강제 형변환이 가능하다.
- `int()` 함수로 float을 int로 강제 형변환이 가능하다.
  - `int()` 함수는 반올림을 하지 않는다. 버린다.
- float 형은 15자리까지 정확하다.
- int형은 임의로 커질 수 있다.
  - C 처럼 32비트 혹은 64비트 크기로 제한되지 않는다. 이보다 더 큰 수를 표현할 수 있다.
- 0 은 False다. 0을 제외한 모든 수는 True다.

### 연산자

- `/` 은 나눗셈의 결과를 float 형으로 return 한다.
- `//` 은 몫을 반환한다.
  - 정수 + 실수(0 <= x < 1)로 표현된다. 그러므로 음수일 땐 마치 올림을 하는 것처럼 보인다.
  - //의 결과가 항상 정수인 것은 아니다. numerator나 denominator가 float 형이면 float 형을 반환한다.
- `**`은 제곱
- `%`은 나머지



### fractions 분수

- 분수를 사용하기 위해선 `import fractions`를 해야한다.

- 분수를 정의하려면 `Fraction` 객체를 생성하고 numerator와 denominator를 전달해야 한다.

  ```python
  import fractions
  x = fractions.Fraction(1, 3)
  ```

- 연산이 가능하다. 결과는 자동으로 약분된다.



### Trigonometry 삼각법

- `import math` 를 사용해 삼각법을 사용할 수 있다.

  ```python
  import math
  
  x = math.pi
  math.sin(math.pi / 2)
  ```



## 3. Strings / 4. Bytes

스트링과 바이트는 양이 많아서 따로 다룬다.



## 5. Lists

- 리스트에는 순서가 있다.

- 인덱스로 접근이 가능하다.

  ```python
  >>> a = list([1,2,3])
  >>> a[0]
  1
  ```

- 음수 인덱스도 가능하다. -1은 맨 뒤를 의미한다.

- Slicing을 통해 리스트의 일부분만을 가져올 수 있다.

  ```python
  >>> a = [1, 2, 3, 4, 5, 6]
  >>> a[1:3]
  [2, 3]
  ```

### List 메소드

- `append` : 리스트 맨 뒤에 더한다.

  - dectructive / no return

  ```python
  >>> a = [1, 2, 3]
  >>> a.append(4)
  [1, 2, 3, 4]
  ```

- `extend` : 매개 변수로 iterable을 받고, 원소 하나하나를 리스트에 추가한다.

  - dectructive / no return

  ```python
  >>> a = [1, 2, 3]
  >>> a.extend([4, 5])
  >>> a
  [1, 2, 3, 4, 5]
  ```

  - append와 다른 점. append는 매개변수로 들어온 값 자체를 리스트에 추가한다.

    ```python
    >>> a = [1, 2, 3]
    >>> a.append([4, 5])
    >>> a
    [1, 2, 3, [4, 5]]
    ```

- `pop` : 맨 뒤에 값을 빼고 해당 값을 반환한다.

  - dectructive / return value

  ```python
  >>> a = [1, 2, 3]
  >>> a.pop()
  3
  >>> a
  [1, 2]
  ```

  - 매개변수로 index 값을 전달하면 해당하는 인덱스의 값을 pop 한다.
  - IndexError를 낸다.

- `remove` : 매개변수로 전달된 값을 제거한다.

  - dectructive / no return

- `count`

  - 매개변수로 전달된 값이 몇개 인지 반환한다.
  - return Value

- `index`

  - 매개변수로 전달된 값의 index를 반환한다. 
  - 해당하는 값이 여러 개일 경우 맨 앞에 있는 것의 위치가 반환된다.
  - return Value

- `insert`

  - 특정 위치에 원하는 값을 넣을 수 있다.
  - dectructive / no return

  ```python
  >>> a = [1, 2, 3]
  >>> a.insert(0, 4)
  >>> a
  [4, 1, 2, 3]
  ```

- `reverse` : 리스트를 뒤집는다.

  - dectructive / no return
  - a.reverse()

- `sort` : 리스트를 오름차순으로 정렬한다.

  - dectructive / no return
  - a.sort()

- `copy`: 얕은 복사

  - return None
  - b = a.copy()

- `clear` : 리스트를 비운다.

  - dectructive / no return
  - a.clear()

## 6. Tuples

- immutable list다. 
- 리스트이기에 인덱스로 접근이 가능하다.
- 메소드로는 count와 index만 있다.
- `list()` 로 리스트로 형변환이 가능하다. 반대도 마찬가지



### 튜플의 장점?

- 리스트보다 빠르다. 상수는 리스트보다 튜플에 넣어두는 게 좋다.
- 데이터의 변화를 막을 수 있어서 안전하다.



## 7. Sets

순서와 중복이 없다. 합집합, 교집합, 차집합 등의 연산이 가능하다.

- `set()` 함수로 집합을 만들 수 있다.

  - 혹은 `{}` 를 사용한다.

  ```python
  a = {1, 2}
  ```

- `{}`만 사용하면 dict다.

  ```python
  >>> a = set()
  >>> type(a)
  set
  >>> a = {}
  >>> type(a)
  dict
  ```

  

### 내장함수

#### modifying Sets

- `add(arg)` : 해당 원소를 집합에 더함
  - destructive / no return

- `discard(arg)` : 해당 원소를 집합에서 제거
  - destructive / no return
  - 만약 해당 원소가 집합에 없어도 아무 문제 안 생김

- `remove(arg)` : 해당 원소를 집합에서 제거
  - destructive / no return
  - 만약 해당 원소가 집합에 없으면 KeyError를 일으킴

- `pop()` : 임의의 원소 하나를 제거
  - destructive / return value

- `clear()` : 집합의 모든 원소를 제거
  - destructive / no return

- `copy(set)` : 얕은 복사



#### 집합 연산

```python
# 사용법
>>> a = {1, 2, 3}
>>> b = {4, 5}
>>> a.union(b)
{1, 2, 3, 4, 5}
```

- `union(set)` : 합집합
  - non-destructive / return set
- `difference(set)` : 차집합
  - non-destructive / return set
- `intersection(set)` : 교집합
  - non-destructive / return set
- `symmetric_difference(set)` : 대칭차집합
  - non-destructive / return set

----

- `update(set)` : 합집합
  - destructive / no return
- `difference_update(set)`: 차집합
  - destructive / no return
- `intersection_update(set)` : 교집합
  - destructive / no return
- `symmetric_difference_update(set)` : 대칭차집합
  - destructive / no return



#### 집합 관계

- `isdisjoint(set)` : 교집합이 Null일 경우 return True
- `issubset(set)` : 부분집합일 경우 return True
- `issupperset(set)` : 상위집합일 경우 return True



## 8. Dictionaries

- 키-값 쌍으로 이루어진 집합. 키는 모두 고유값이기에 중복이 불가능하다.
- `a = dict()` 로 a를 딕셔너리로 선언할 수 있다.
- `a[key] = value` 형식으로 딕셔너리에 값을 추가할 수 있다.
- key로 value에 접근할 수 있지만 value로 key에 접근할 수 없다.
  - `a[key]` 로 접근한다. 해당하는 key가 없으면 KeyError를 낸다.



### 내장함수

- `get(arg)` : 특정 키에 해당하는 값을 가져옴. 해당 키가 없을 경우 None을 return
  - non-destructive / return Value or None

- `items(arg)` : 리스트를 반환. 요소들은 key, value로 된 튜플
  - non-destructive / return dict_items
- `values()` : 리스트를 반환
  - non-destructive / return dict_values
- `keys()` : 리스트를 반환
  - non-destructive / return dict_keys
- `update(dict)` : 두 dict를 합침
  - dectructive / no return

---

- `setdefault(key, value)` : 딕셔너리에 요소를 추가.
  - 이미 값이 있으면 값을 바꾸지는 않음
  - value를 적지 않으면 `key: None` 형태로 추가됨
  - destructive / return Value

- `fromkeys(iterable)` : iterable의 요소들을 key로, 각 key에는 value를 None으로 만드는 딕셔너리를 반환.
  - non-destructive / return dict

---

- `clear()`  : 모든 키와 값을 제거
  - destructive / no return
- `copy()` : 얕은 복사
  - non-destructive / no return

- `pop(key)`  : 해당하는 key를 제거하고 value를 return
  - 해당하는 key가 없으면 KeyError
  - destructive / return valule

- `popitem()` : 임의 원소를 제거하고 튜플로 key와 value를 return
  - destructive / return Tuple



## \+ 9. None

- None은 null value와 같다. 
- None은 False가 아니다. 그렇다고 True도 아니다.
- None은 0이 아니다. 
- None은 empty string이 아니다.



#### 참고

- [dive into](https://diveinto.org/python3/native-datatypes.html)

