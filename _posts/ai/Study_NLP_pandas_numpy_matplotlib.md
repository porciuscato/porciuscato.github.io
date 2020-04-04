# 딥러닝을 위한 자연어 처리 입문

[위키독스](https://wikidocs.net/22488)

데이터 분석을 위한 필수 패키지 삼대장이 있다. 바로 Pandas와 Numpy 그리고 Matplotlib다. 세 개의 패키지 모두 아나콘다를 설치했다면 자동으로 설치되어져 있다. 

## 1. 판다스

판다스(Pandas)는 파이썬 데이터 처리를 위한 라이브러리다. 파이썬을 이용한 데이터 분석과 같은 작업에서 필수 라이브러리로 알려져있다. 참고 할 수 있는 Pandas [링크](http://pandas.pydata.org/pandas-docs/stable/)다.

Pandas는 주로 pd라는 명칭으로 임포트한다.

```python
import pandas as pd
```

Pandas는 총 세 가지 데이터 구조를 사용한다.

1. 시리즈(Series)

2. 데이터프레임(DataFrame)

3. 패널(Panel)

### 1) 시리즈

시리즈 클래스는 1차원 배열의 값(values)에 각 값에 대응되는 인덱스(index)를 부여할 수 있는 구조를 갖고 있다.

```python
sr = pd.Series([17000, 18000, 1000, 5000],
       index=["피자", "치킨", "콜라", "맥주"])
print(sr)
```

```
피자    17000
치킨    18000
콜라     1000
맥주     5000
dtype: int64
```

```python
print(sr.values)
```

```
[17000 18000  1000  5000]
```

```python
print(sr.index)
```

```
Index(['피자', '치킨', '콜라', '맥주'], dtype='object')
```

### 2) 데이터프레임

데이터프레임은 2차원 리스트를 매개변수로 전달한다. 2차원이므로 행방향 인덱스(index)와 열방향 인덱스(column)가 존재한다. 즉, 행과 열을 가지는 자료구조입니다. 시리즈가 인덱스(index)와 값(values)으로 구성된다면, 데이터프레임은 열(columns)까지 추가되어 열(columns), 인덱스(index), 값(values)으로 구성된다.

```python
values = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
index = ['one', 'two', 'three']
columns = ['A', 'B', 'C']

df = pd.DataFrame(values, index=index, columns=columns)
print(df)
```

```
       A  B  C
one    1  2  3
two    4  5  6
three  7  8  9
```

```python
print(df.index) # 인덱스 출력
print(df.columns) # 열 출력
print(df.values) # 값 출력
```

#### (1) 데이터프레임 생성

데이터프레임은 리스트(List), 시리즈(Series), 딕셔너리(dict), Numpy의 ndarrays, 또 다른 데이터프레임으로 생성할 수 있다. 여기서는 리스트와 딕셔너리를 통해서 데이터프레임을 생성 해보자.

```python
# 리스트로 생성하기
data = [
    ['1000', 'Steve', 90.72], 
    ['1001', 'James', 78.09], 
    ['1002', 'Doyeon', 98.43], 
    ['1003', 'Jane', 64.19], 
    ['1004', 'Pilwoong', 81.30],
    ['1005', 'Tony', 99.14],
]
df = pd.DataFrame(data)
print(df)
```

```
      0         1      2
0  1000     Steve  90.72
1  1001     James  78.09
2  1002    Doyeon  98.43
3  1003      Jane  64.19
4  1004  Pilwoong  81.30
5  1005      Tony  99.14
```

columns 지정이 가능하다.

```python
df = pd.DataFrame(data, columns=['학번', '이름', '점수'])
# 혹은
df.columns = ['학번', '이름', '점수']
```

이제 딕셔너리롤 생성해보자

```python
# 딕셔너리로 생성하기
data = { '학번' : ['1000', '1001', '1002', '1003', '1004', '1005'],
'이름' : [ 'Steve', 'James', 'Doyeon', 'Jane', 'Pilwoong', 'Tony'],
         '점수': [90.72, 78.09, 98.43, 64.19, 81.30, 99.14]}

df = pd.DataFrame(data)
print(df)
```

```
     학번        이름     점수
0  1000     Steve  90.72
1  1001     James  78.09
2  1002    Doyeon  98.43
3  1003      Jane  64.19
4  1004  Pilwoong  81.30
5  1005      Tony  99.14
```

#### (2) 데이터프레임 조회하기

원하는 구간만 확인하는 명령어는 다음과 같은 것들이 있다.

```python
# df의 타입은 pandas.core.frame.DataFrame
df.head(n) # 앞 부분을 n개만 보기
df.tail(n) # 뒷 부분을 n개만 보기
df['열이름'] # 해당되는 열을 확인
```

#### (3) 외부 데이터 읽기

`pd.read_csv()`

```python
df=pd.read_csv('example.csv 파일의 경로') # example.csv 파일 읽기
# 예를 들어 윈도우 바탕화면에서 작업한 저자의 경우
# df=pd.read_csv(r'C:\Users\USER\Desktop\example.csv')였습니다.
print(df)
```



### 3) Pandas Profiling

좋은 머신 러닝 결과를 얻기 위해서는 데이터의 성격을 파악하는 과정이 선행되어야 한다. 이 과정에서 데이터 내 값의 분포, 변수 간의 관계, Null 값과 같은 결측값(missing values) 존재 유무 등을 파악하게 되는데 이와 같이 데이터를 파악하는 과정을 **EDA(Exploratory Data Analysis, 탐색적 데이터 분석)**이라고 한다다. 방대한 양의 데이터를 가진 데이터프레임을 .profile_report()라는 단 한 줄의 명령으로 탐색하는 패키지인 판다스 프로파일링(pandas-profiling)이 있다.

```bash
pip install -U pandas-profiling
```

#### (1)  파일 불러오기

예시 파일을 가져와보자. [링크](https://www.kaggle.com/uciml/sms-spam-collection-dataset)

파일을 다음처럼 불러올 수 있다.

```python
import pandas as pd
import pandas_profiling
data = pd.read_csv('spam.csv 파일의 경로',encoding='latin1')
# 윈도우 바탕화면에서 작업한 경우에는
# data = pd.read_csv(r'C:\Users\USER\Desktop\spam.csv',encoding='latin1')
```

#### (2) 리포트 생성하기

```python
pr=data.profile_report() # 프로파일링 결과 리포트를 pr에 저장
```

결과를 파일로 저장해서 열어보자

```python
pr.to_file('./pr_report.html') # pr_report.html 파일로 저장
```





---



## 2. 넘파이

넘파이(Numpy)는 수치 데이터를 다루는 파이썬 패키지다. Numpy의 핵심이라고 불리는 다차원 행렬 자료구조인 ndarray를 통해 벡터 및 행렬을 사용하는 선형 대수 계산에서 주로 사용된다. Numpy는 편의성뿐만 아니라, 속도면에서도 순수 파이썬에 비해 압도적으로 빠르다는 장점이 있다.

np로 임포트하는 것이 관례다.

```python
import numpy as np
```

주요 모듈은 다음과 같다.

1. `np.array()` # 리스트, 튜플, 배열로 부터 ndarray를 생성
2. `np.asarray()` # 기존의 array로 부터 ndarray를 생성
3. `np.arange()` # range와 비슷
4. `np.linspace(start, end, num)` # [start, end] 균일한 간격으로 num개 생성
5. `np.logspace(start, end, num)` # [start, end] log scale 간격으로 num개 생성

#### 1) np.array()

Numpy의 핵심은 ndarray다. np.array()는 리스트, 튜플, 배열로 부터 ndarray를 생성한다. 또한 인덱스가 항상 0으로 시작한다는 특징을 갖고 있다.

```python
a = np.array([1, 2, 3, 4, 5]) #리스트를 가지고 1차원 배열 생성
print(type(a))
print(a)
```

```
<type 'numpy.ndarray'>
array([1, 2, 3, 4, 5])
```

2차 배열을 만들어보자

```python
b = np.array([[10, 20, 30], [ 60, 70, 80]]) 
print(b)
```

```
array([[10, 20, 30],
       [60, 70, 80]])
```

- `ndim` : 행렬의 차원을 반환

- `shape`: 행렬의 크기를 반환

  ```python
  print(b.ndim) #차원 출력
  print(b.shape) #크기 출력
  ```

  ```
  2
  (2, 3)
  ```

  

#### 2) ndarray 초기화

`np.array()` 이외 다른 방법으로도 ndarray를 생성할 수 있다.

- `nd.zeroes(size)` : 모두 0인 배열

- `nd.ones(size)` : 모두 1인 배열

- `nd.full(size, value)`: 사용자가 지정한 값으로 채움

- `nd.eye(value)` : 대각행렬 생성

- `np.random.random(size)` : 임의의 값으로 채워진 배열 생성

  ```python
  a = np.zeros((2,3)) # 모든값이 0인 2x3 배열 생성.
  print(a)
  ```

  ```
  [[0. 0. 0.]
   [0. 0. 0.]]
  ```

  ```python
  a = np.ones((2,3)) # 모든값이 1인 2x3 배열 생성.
  print(a)
  ```

  ```
  [[1. 1. 1.]
   [1. 1. 1.]]
  ```

  ```python
  a = np.full((2,2), 7) # 모든 값이 특정 상수인 배열 생성. 이 경우에는 7.
  print(a)
  ```

  ```
  [[7 7]
   [7 7]]
  ```

  ```python
  a = np.eye(3) # 대각선으로는 1이고 나머지는 0인 2차원 배열을 생성.
  print(a)
  ```

  ```
  [[1. 0. 0.]
   [0. 1. 0.]]
   [0. 0. 1.]]
  ```

  ```python
  a = np.random.random((2,2)) # 임의의 값으로 채워진 배열 생성
  print(a)
  ```

  ```
  [[0.3111881  0.72996102]
   [0.65667734 0.40758328]]
  ```

### 3) np.arange()

지정해준 범위에 대해 배열을 생성

- `np.arange(start, stop, step, dtype)`

  ```python
  a = np.arange(10) #0부터 9까지
  print(a)
  ```

  ```
  [0 1 2 3 4 5 6 7 8 9]
  ```

  ```python
  a = np.arange(1, 10, 2) #1부터 9까지 +2씩 적용되는 범위
  print(a)
  ```

  ```
  [1 3 5 7 9]
  ```

### 4) reshape()

```python
a = np.array(np.arange(30)).reshape((5,6))
print(a)
```

```
[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]
 [18 19 20 21 22 23]
 [24 25 26 27 28 29]]
```

### 5) Numpy Slicing

```python
import numpy as np
a = np.array([[1, 2, 3], [4, 5, 6]])
b=a[0:2, 0:2]
print(b)
```

```
[[1 2]
 [4 5]]
```

```python
b=a[0, :] # 첫번째 행 출력
print(b)
```

```
[1 2 3]
```

```python
b=a[:, 1] # 두번째 열 출력
print(b)
```

```
[2 5]
```

### 6) Numpy 정수 인덱싱

```python
a = np.array([[1,2], [4,5], [7,8]])
b = a[[2, 1],[1, 0]] # a[[row2, row1],[col1, col0]]을 의미함.
print(b)
```

```
[8 4]
```

### 7) Numpy 연산

연산을 할 수 있다. 

\+ , \-, \*, / 의 연산자를 사용할 수 있으며

add(), substract(), multiply(), divide() 함수를 사용할 수 있다.

- `dot()` : 행렬곱을 할 수 있다.

```python
x = np.array([1,2,3])
y = np.array([4,5,6])
b = x + y # 각 요소에 대해서 더함
# b = np.add(x, y)와 동일함

b = x - y # 각 요소에 대해서 빼기
# b = np.substract(x, y)와 동일함

b = b * x # 각 요소에 대해서 곱셈
# b = np.multiply(b, x)와 동일함

b = b / x # 각 요소에 대해서 나눗셈
# b = np.divide(b, x)와 동일함
```

```python
## 행렬곱
a = np.array([[1,2],[3,4]])
b = np.array([[5,6],[7,8]])

c = np.dot(a, b)
```

```
[[19 22]
 [43 50]]
```



---



## 3. Matplotlib

맷플롯립(Matplotlib)은 데이터를 차트(chart)나 플롯(plot)으로 시각화(visulaization)하는 패키지다. 데이터 분석에서 Matplotlib은 데이터 분석 이전에 데이터 이해를 위한 시각화나, 데이터 분석 후에 결과를 시각화하기 위해서 사용된다.

주피터 노트북에서 사용하기 위해선 `%matplotlib inline`을 써야 한다. 그림을 표시하도록 지정한다.

```python
%matplotlib inline
import matplotlib.pyplot as plt
```

### 1) 라인 플롯 그리기

plot()은 라인 플롯을 그리는 기능을 수행한다. plot() X축과 Y축의 값을 기재하고 그림을 표시하는 show()를 통해서 시각화해보자. 그래프에는 제목을 지정해줄 수 있는데 이 경우에는 title('원하는 제목')을 사용한다.

```python
plt.title('test')
plt.plot([1,2,3,4],[2,4,8,6])
plt.show()
```

축에 레이블도 넣을 수 있다.

```python
plt.title('test')
plt.plot([1,2,3,4],[2,4,8,6])
plt.xlabel('hours')
plt.ylabel('score')
plt.show()
```

동시에 여러 개의 plot()을 사용하여 하나의 그래프에 나타낼 수 있다. 각 선이 어떤 데이터를 나타내는지 범례(legend)를 사용할 수 있다.

```python
plt.title('students')
plt.plot([1,2,3,4],[2,4,8,6])
plt.plot([1.5,2.5,3.5,4.5],[3,5,8,10]) #라인 새로 추가
plt.xlabel('hours')
plt.ylabel('score')
plt.legend(['A student', 'B student']) #범례 삽입
plt.show()
```

