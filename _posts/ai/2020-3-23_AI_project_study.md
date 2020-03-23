---
comments: true
title: AI study
published: false
updated: 2020-3-23
tags: [AI]
categories: [development]
---

AI 개발에 대해 공부해보자. 다양한 머신러닝 방법 중 신경망 네트워크(Neural Network), 그 중 심층 신경망 네트워크(Deep Neural Network)를 사용해 이미지 처리와 자연어 처리를 공부하자. 찾아보기 좋은 키워드는 Detection, Obejct Tracking, Video Captioning, Machine Translation, Text Summarization 등이 있다.



#### 키워드

선형 회귀(Linear Regression), 신경망 네트워크(Neural Network)



#### 주요 기술 스택

| 분류     | 기술 스택/ 도구 | 버전     | 비고                    |
| -------- | --------------- | -------- | ----------------------- |
| 언어     | Python          | 3.7.6    | Anaconda 가상환경       |
| 머신러닝 | Numpy           | 1.18.1   |                         |
|          | Scipy           | 1.4.1    |                         |
|          | Scikit-learn    | 0.22.1   |                         |
| 딥러닝   | Tensorflow      | 2.0.0    | Deep Learning Framework |
|          | Keras           | 2.2.4-tf | High Level API          |
| 시각화   | Matplotlib      | 3.1.3    |                         |
|          | Tensorboard     | 2.1.0    | TensorFlow 시각화 툴킷  |
| 기타     | Anaconda        | 4.8.2    | 패키지 관리 및 가상환경 |
|          | tqdm            | 4.42.1   | 반복문 진척도 시각화    |



## 주요 개념 학습

### 머신러닝, 딥러닝

- 인공지능은 인간의 지능을 컴퓨터로 구현한 것. 머신러닝은 인공 지능 시스템을 구현하는 구체적인 접근 방식
- 인공 신경망 모델: 머신 러닝 방법 중 생물학적 신경망의 시냅스 결합을 모방한 모델
  - 더 복잡하고 다양한 특성(feature) 정보를 얻기 위해 2개 이상의 신경망 층을 쌓은 모델을 심층 신경망(Deep Neural Network)라고 한다. 이러한 심층 신경망을 사용한 머신러닝을 딥러닝으로 부른다.

| 주제     | 내용                                                   | 링크                                                         |
| -------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| 인공지능 | 인공지능의 개념, 역사와 단계별 인공지능에 대한 설명    | [:link:](https://brunch.co.kr/@gdhan/1)                      |
|          | 인공지능과 이에 포함된 세부 카테고리에 대한 설명       | [:link:](https://saintbinary.tistory.com/21)                 |
| 머신러닝 | 머신러닝의 3가지 분야 및 알고리즘 분류 표              | [:link:](https://swalloow.github.io/pyml-intro1)             |
|          | 2018년도에 나온 유용한 머신러닝 프로젝트들에 대한 설명 | [:link:](https://tykimos.github.io/2019/01/06/2018_ML_projects/) |
| 딥러닝   | 딥러닝 모델을 적용한 다양한 프로젝트와 활용 사례       | [:link:](https://brunch.co.kr/@itschloe1/23)                 |



### 선형회귀

선형회귀는 모델을 1차 함수의 형태로 선택한 것이다. y = wx + b 일 경우 이 모델에 대해 최적의 변수, 즉 최적의 기울기와 편차를 찾아내야 한다.

최적화 함수는 평균 제곱 편차(Mean Squared Error)가 가장 작은 함수다. MSE는 다음의 식으로 계산한다.
$$
MSE = \frac{1}{n}\sum_{i=1}^n(y_i-y_i^*)^2
$$
손실을 최소로 만드는 기울기와 편차를 찾는 것이 최적화 함수가 하는 일이다. 대표적인  최적화 방법으로는 경사 하강법(Gradient Descent)이 있다.

자세한 내용은 아래 링크를 참고하자.

| 주제        | 내용                                  | 링크                                                  |
| ----------- | ------------------------------------- | ----------------------------------------------------- |
| 경사 하강법 | 수학적인 부분에 초점을 맞춘 설명 영상 | [:link:](https://www.youtube.com/watch?v=ve6gtpZV83E) |



### 신경망 네트워크(Neural Network)

선형 모델로만 파악하기 어려운 알고리즘을 신경망 네트워크로 구현할 수 있다. 

컴퓨터가 2012년 경부터 이미지를 통한 강아지, 고양이를 분리하기 시작하더니 지금은 비약적으로 발전한 상태다. 여기에 사용된 기술이 인공 신경망, 그 중 컨볼루션 인공 신경망(Convolution Neural Network)이었다. CNN과 RNN(Recurrent Neural Network)을 다루기 전에 인공 시경망 모델을 학습해야 한다.

| 주제          | 내용                                                   | 링크                                                         |
| ------------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| 뉴럴 네트워크 | 신경망에 대한 시각적인 설명(신경망의 구조)             | [:link:](https://www.youtube.com/watch?v=aircAruvnKk)        |
|               | 신경망이 학습되는 과정을 설명(경사 하강법)             | [:link:](https://www.youtube.com/watch?v=IHZwWFHWa-w)        |
|               | 역전파의 개념과 실제 계산 과정에 대한 설명             | [:link:](https://www.youtube.com/watch?v=Ilg3gGewQ5U)        |
| 손실함수      | 대표적인 손실 함수에 대한 설명과 손실 함수를 쓰는 이유 | [:link:](https://eehoeskrap.tistory.com/145)                 |
|               | 크로스 앤트로피 함수에 대한 설명과 사용 이유           | [:link:](https://www.youtube.com/watch?v=uMYhthKw1PU)        |
| 활성화 함수   | 활성화 함수를 사용하는 이유와 코드 구현 예시           | [:link:](https://m.blog.naver.com/PostView.nhn?blogId=worb1605&logNo=221187949828&proxyReferer=https%3A%2F%2Fwww.google.com%2F) |
|               | 다양한 활성화 함수와 이를 시각화 한 그래프             | [:link:](https://reniew.github.io/12/)                       |
|               | Vanishing Gradient 문제와 이를 해결한 활성화 함수      | [:link:](https://gomguard.tistory.com/183)                   |
| 최적화 함수   | 한번에 사용하는 데이터 수에 따른 경사하강법의 종류     | [:link:](https://bioinformaticsandme.tistory.com/134)        |
|               | 다양한 경사하강 알고리즘과 각각의 특성                 | [:link:](https://twinw.tistory.com/247)                      |
| 딥러닝        | 딥러닝에 대한 전반적인 설명                            | [:link:](http://research.sualab.com/introduction/2017/10/10/what-is-deep-learning-1.html) |



### Python

다양한 빅데이터 알고리즘 등이 있고 구글의 TensorFlow와 페이스북의 PyTorch의 영향으로 파이썬이 널리 사용되고 있다.

| 주제   | 내용         | 링크                                                         |
| ------ | ------------ | ------------------------------------------------------------ |
| Python | 공식홈페이지 | [:link:](https://www.python.org/)                            |
|        | 기초 강의    | [:link:](https://wikidocs.net/book/1)                        |
|        | 온라인 강의  | [:link:](https://www.udacity.com/course/introduction-to-python--ud1110) |



### 주요 라이브러리 및 프레임워크

| 주제       | 내용                                                     | 링크                                                         |
| ---------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| Python     | 공식 홈페이지                                            | [:link:](https://numpy.org/)                                 |
|            | 기초 사용법                                              | [:link:](http://taewan.kim/post/numpy_cheat_sheet/)          |
| Matplotlib | 공식 홈페이지                                            | [:link:](https://matplotlib.org/)                            |
|            | 공식 튜토리얼                                            | [:link:](https://matplotlib.org/tutorials/index.html)        |
|            | Matplotlib를 더 편리하게 사용할 수 있게 도와주는 Seaborn | [:link:](https://seaborn.pydata.org/)                        |
| TensorFlow | 공식 홈페이지                                            | [:link:](https://www.tensorflow.org/)                        |
|            | 공식 튜토리얼                                            | [:link:](https://www.tensorflow.org/tutorials)               |
| Keras      | 공식 홈페이지                                            | [:link:](https://keras.io/ko/)                               |
|            | 회귀 문제 튜토리얼                                       | [:link:](https://www.tensorflow.org/tutorials/keras/regression) |

## 개발환경 설정

### 1. 아나콘다

#### 1) 설치

[링크](https://www.anaconda.com/distribution/)에 들어가 운영체제에 맞는 아나콘다 버전을 다운받는다.

> 아나콘다를 사용하는 이유가 무엇인가?

#### 2) 아나콘다 가상 환경 생성 및 활성화

```
conda create -n AI python=3.7
conda activate AI
```

#### 3) TensorFlow 및 필요 라이브러리 설치

```
conda install git matplotlib scikit-learn tqdm scipy numpy tensorflow-gpu==2.0.0
```



### 참고 자료 ​

#### 1) Deep Learning For Regression Problem

| 주제               | 내용      | 링크                                                         |
| ------------------ | --------- | ------------------------------------------------------------ |
| 주택 가격 예측하기 | 예제 설명 | [:link:](https://towardsdatascience.com/deep-neural-networks-for-regression-problems-81321897ca33) |
|                    | 코드 자료 | [:link:](https://colab.research.google.com/drive/1J8ZTI2UIJCwml2nrLVu8Gg0GXEz-7ZK0) |
|                    | 데이터셋  | [:link:](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data) |

#### 2) 공개 데이터셋 및 딥 러닝 프레임워크

| 주제          |                                                              |
| ------------- | ------------------------------------------------------------ |
| 공개 데이터셋 | [한국정보화진흥원](http://www.aihub.or.kr/)                  |
|               | [코드 자료](https://colab.research.google.com/drive/1J8ZTI2UIJCwml2nrLVu8Gg0GXEz-7ZK0) |
|               | [데이터셋](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data) |
| Kaggle        | [캐글이란](https://musma.github.io/2019/03/04/about-kaggle.html) |
|               | [컴페티션 목록](https://www.kaggle.com/competitions)         |
|               | [데이터셋](https://www.kaggle.com/datasets)                  |
| PyTorch       | [텐서플로우와 비교](https://devlog.jwgo.kr/2019/10/17/tensorflow-vs-pytorch/) |
|               | [홈페이지](https://pytorch.org/)                             |
|               | [강의자료](https://github.com/GunhoChoi/PyTorch-FastCampus)  |
| 기타          | [데이터 사이언스](https://blog.ab180.co/data-science-with-r-1-misperception/) |
|               | [딥러닝 공부 자료 모음](https://bbongcol.github.io/deep-learning-bookmarks/) |

