# 인공지능 프로젝트

 - 이미지 데이터 다운로드: [https://i02lab1.p.ssafy.io/images.zip (4.07GB)](https://i02lab1.p.ssafy.io/images.zip)
 - 다운로드 받은 파일을 datasets 폴더에서 압축 해제

# 차례

1. [단순 선형 회귀 모델 구현](#1. 단순 선형 회귀 모델 구현)

2. [이미지 캡셔닝 Configuration](#2. 이미지 캡셔닝 Configuration)
3. [이미지 캡셔닝 데이터 전처리](#3. 이미지 캡셔닝 데이터 전처리)



# 1. 단순 선형 회귀 모델 구현

## 1-1 데이터 읽기 밎 시각화

### 상세 내용

- Numpy, Matplotlib 라이브러리 사용
- datasets/linear_train.npy 데이터셋 읽어오기
- x 축, y 축 데이터 열을 가진 데이터셋 확인
- 데이터 시각화

### 내용 정리

#### 1) 환경설정

어제는 conda prompt로 conda 가상환경을 설정했다. 이제 이를 vscode에서 실행하는 방법에 대해 알아보자.

##### Code-Runner 설치

- VS code extension인 Code-Runner를 설치한다.
  - `ctrl + shift + x` -> `code runnser` 검색 -> VS code 재시작

##### 코드 실행

- `ctrl + shift + p` -> `Python: select interpreter` 검색 -> conda 가상환경 선택
- 실행하려면 `ctrl + alt + n` : run python file in terminal과 같다.



#### 2) npy 파일 읽기

- npy 파일은? numpy 라이브러리를 통해 데이터를 저장한 파일을 일컫는다. 

- npy로 저장하고 불러오기

  ```python
  ####  예시코드 ####
  import numpy as np
  
  # 저장하는 numpy 데이터
  save_data = np.arrange(100)
  
  # numpy.ndarray 저장. 
  np.save("data.npy", save_data) # @파일명, @값
  
  # 불러오기
  load_data = np.load("data.npy") # @파일명
  ```



#### 3) 시각화 하기

읽어온 npy 파일을 matplotlib를 사용해 표로 나타내보자.

```python
import numpy as np
from matplotlib import pyplot as plt

data = np.load("datasets/linear_train.npy")
x_data = np.expand_dims(data[:,0], axis=1) # x축
y_data = data[:,1] # y축

plt.title("Example")
plt.xlabel("x axis")
plt.ylabel("y axis")
plt.plot(x_data, y_data, 'bo')
plt.show()
```



#### 4) 결과

<center><img src="img/1_1_result.jpg"></center>



#### 참고

[numpy tutorials](https://www.tutorialspoint.com/numpy/numpy_matplotlib.htm)

[matplotlib tutorials](https://matplotlib.org/tutorials/introductory/pyplot.html)



## 1-2 선형 모델 클래스 구현

### 상세 내용

- 위치: models/linear_model.py

- Class명: LinearModel()
- LinearModel 클래스는 tf.keras.Model을 상속
- call() 호출 시, 입력 값에 대한 결과 값을 리턴

```python
from models.linear_model import LinearModel
import numpy as np

train_data = np.load("datasets/linear_train.npy")
model = LinearModel(num_units=1)

x_data = np.expand_dims(train_data[:,0], axis=1)

print(model.call(train_data))
```

> train_data는 학습시킬 데이터로서 이미 각 x에 대해 y 값이 정해져있는 상태다. 여기서 만든 모델이 이 데이터를 학습하여 x 값만 주어졌을 때 결과를 낼 수 있어야 한다.



## 1-3 최적화 함수 및 손실 함수 바인딩

### 상세 내용

- 모델에 최적화 함수 및 손실 함수를 바인딩한다.

  ```python
  from models.linear_model import LinearModel
  import tensorflow as tf
  import numpy as np
  
  # 학습시킬 데이터
  train_data = np.load("datasets/linear_train.npy")
  
  # Dense는 한 번이다.
  model = LinearModel(num_units=1)
  
  # 최적화 함수 및 손실 함수를 바인딩시킨다.
  model.compile(optimizer=tf.keras.optimizers.SGD(learning_rate=0.001),
  			  loss=tf.keras.losses.MSE,
  			  metrics=[tf.keras.metrics.MeanSquaredError()])
  ```

  



## 1-4 모델 학습 함수 구현

### 상세 내용

- 학습 데이터를 x축, y축에 넣어 모델을 학습시킨다.
- x: x축 데이터 / y: y축 데이터 / epochs: 데이터 전체에 대한 학습 반복 횟수
- batch_size: 배치의 크기

```python
from models.linear_model import LinearModel
import tensorflow as tf
import numpy as np

# 학습시킬 데이터
train_data = np.load("datasets/linear_train.npy")

# tf 형식에 맞게 변환
x_data = np.expand_dims(train_data[:,0], axis=1) # x축
y_data = train_data[:,1] # y축

# Dense는 한 번이다.
model = LinearModel(num_units=1)

# 최적화 함수 및 손실 함수를 바인딩시킨다.
model.compile(optimizer=tf.keras.optimizers.SGD(learning_rate=0.001),
			  loss=tf.keras.losses.MSE,
			  metrics=[tf.keras.metrics.MeanSquaredError()])

# 모델 학습
model.fit(x=x_data, 
		  y=y_data, 
		  epochs=10, 
		  batch_size=32)
```



## 1-5 예측 및 결과 시각화

### 상세 내용

- 새로운 입력을 받으면 학습된 변수를 이용해 예측 값을 리턴하는 함수 구현
- 테스트 입력 값을 읽어와 예측값을 구하고 시각화

```python
from models.linear_model import LinearModel
import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt


#### 모델 학습 ####
train_data = np.load("datasets/linear_train.npy")
x_data = np.expand_dims(train_data[:,0], axis=1) # x축
y_data = train_data[:,1] # y축

model = LinearModel(num_units=1)

model.compile(optimizer=tf.keras.optimizers.SGD(learning_rate=0.001),
			  loss=tf.keras.losses.MSE,
			  metrics=[tf.keras.metrics.MeanSquaredError()])

model.fit(x=x_data, 
		  y=y_data, 
		  epochs=10, 
		  batch_size=32)

#### 모델 테스트 ####
# 테스트에 사용할 x 값
test_x = np.load("datasets/linear_test_x.npy")

# x의 결과값
prediction = model.predict(x=test_x,
    					   batch_size=None)

# 결과 시각화
plt.scatter(x_data, y_data, s=5, label="train data") # 학습 데이터
plt.scatter(test_x, prediction, s=5, label="prediction data") # 예측 데이터
plt.legend()
plt.show()


# 모델 정리
model.summary()
```

### 결과

<center><img src="img/1_5_result.jpg"></center>



# 2. 이미지 캡셔닝 Configuration

## 2-1 config.py 파일 구현

### 상세 내용

- 이미지 캡셔닝 모델 구현에 필요한 세팅 값들을 저장해 놓은 config.py 파일 생성(argparse 모듈)

- 캡션 데이터가 저장된 csv 파일, 실제 이미지 파일등리 저장된 경로 등을 추가

```python
import argparse

# parser를 생성
parser = argparse.ArgumentParser()
# 캡션 데이터 경로를 저장
parser.add_argument( 
    "--caption_file_path", 
    type=str, default="./datasets/aptions.csv"
)
# 이미지 파일의 경로를 저장
parser.add_argument(
    "--image_file_path", 
    type=str, default="./datasets/images"
)

args = parser.parse_args()
```

클래스의 속성값을 불러오듯 위의 설정들을 불러올 수 있다.

```python
args.caption_file_path # './datasets/aptions.csv' 반환
args.image_file_path # './datasets/images' 반환
```



## 2-2 세팅 값 저장

### 상세 내용

- Configuration 변수들은 추후 다양하게 바꿔가며 실험되기 때문에 train.py를 실행할 때마다 당시의 세팅 값들을 저장하는 함수를 구현해야 한다.
- 이를 utils/utils.py 에 구현한다.

```python
import sys
# config 파일을 불러오기 위한 경로 추가
sys.path.append(os.path.dirname(os.path.dirname(os.path.abspath(__file__))))
from config import parser


# Req. 2-2	세팅 값 저장
def save_config(command, path):
	parser.add_argument(command, type=str, default=path)
	args = parser.parse_args()
```

save_config 함수는 인자로 command 와 path를 받아서 config.py에서 설정한 parser에 argument를 추가한다. 



# 3. 이미지 캡셔닝 데이터 전처리

## 3-1 이미지 경로 및 캡션 불러오기

### 상세 내용

- 캡션 파일을 읽어와 이미지 파일 경로와 캡션을 리턴하는 함수를 구현한다.
- 이미지 파일 이름과 각 파일에 해당하는 캡션이 저장된 csv 파일을 읽어온다.
- 파일에 있는 이미지 파일 이름과 캡션을 분리해 각각을 리스트로 만들어 리턴한다.

