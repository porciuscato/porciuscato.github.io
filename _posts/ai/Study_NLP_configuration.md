# 딥러닝을 위한 자연어 처리 입문

[위키독스](https://wikidocs.net/22488)

## NLP 위한 환경설정

아나콘다 혹은 코랩에서 진행한다.

### 1. 아나콘다 설치

[링크](https://www.anaconda.com/distribution/)

아나콘다 설치 후 프롬프트를 열어 파이썬 패키지를 전부 최신화 한다.

```
conda update -n base conda
conda update --all
```

### 2. 구글 Colab

인터넷만 된다면 주피터 노트북 같은 환경을 바로 만들 수 있다.

코랩 [링크](https://colab.research.google.com/)

코랩의 사용법 [영상](https://youtu.be/inN8seMm7UI)

코랩의 사용법 [블로그](https://tykimos.github.io/2019/01/22/colab_getting_started/)

코랩에 파일 업로드, 다운로드 하는 [방법](http://www.dreamy.pe.kr/zbxe/CodeClip/3769485)

### 3. 필요 라이브러리

Numpy, Pandas, Jupyter notebook, scikit-learn, matplotlib, seaborn, nltk 등이 필요한데 아나콘다에 설치되어 있다. 아나콘다에 설치되지 않은 tensorflow, keras, gensim을 설치한다.

#### 1) tensorflow

텐서플로우는 구글이 2015년에 공개한 머신 러닝 오픈소스 라이브러리다. 머신 러닝과 딥 러닝을 직관적이고 손쉽게 할 수 있도록 설계되었다.

```bash
> pip install tensorflow
```

ipython 쉘을 실행하여 버전을 확인해보자.

```bash
> ipython
...
In [1]: import tensorflow as tf
In [2]: tf.__version__
Out[2]: '2.0.0
```

#### 2) keras

케라스(Keras)는 딥 러닝 프레임워크인 텐서플로우에 대한 추상화 된 API를 제공한다 케라스는 백엔드로 텐서플로우를 사용하며, 좀 더 쉽게 딥 러닝을 사용할 수 있게 해준다. 쉽게 말해, 텐서플로우 코드를 훨씬 간단하게 작성할 수 있다.

```bash
> pip install keras
```

```
> ipython
...
In [1]: import gensim
In [2]: gensim.__version__
Out[2]: '3.8.1'
```

#### 3) gensim

젠심(Gensim)은 머신 러닝을 사용하여 토픽 모델링과 자연어 처리 등을 수행할 수 있게 해주는 오픈 소스 라이브러리다. 

```
> pip install gensim
```

```
> ipython
...
In [1]: import gensim
In [2]: gensim.__version__
Out[2]: '3.8.1'
```

#### 4) Scikit-learn

사이킷런(Scikit-learn)은 파이썬 머신러닝 라이브러리다. 사이킷런을 통해 나이브 베이즈 분류, 서포트 벡터 머신 등 다양한 머신 러닝 모듈을 불러올 수 있다. 또한, 사이킷런에는 머신러닝을 연습하기 위한 아이리스 데이터, 당뇨병 데이터 등 자체 데이터 또한 제공하고 있다. 사이킷런은 위 패키지들과 달리 아나콘다로 자동 설치되지만 아나콘다를 설치하지 않았다면 아래의 커맨드로 Scikit-learn을 별도 설치할 수 있다.

```
> pip install scikit-learn
```

```
> ipython
...
In [1]: import sklearn
In [2]: sklearn.__version__
Out[2]: '0.21.3'
```

### 4. 자연어 처리를 위한 NLTK와 KoNLPy 설치하기

#### 1) NLTK와 NLTK Data 설치

엔엘티케이(NLTK)는 자연어 처리를 위한 파이썬 패키지다. 아나콘다를 설치하였다면 NLTK는 기본적으로 설치가 되어있다. 아나콘다를 설치하지 않았다면 아래의 커맨드로 NLTK를 별도 설치할 수 있다.

```sql
> pip install nltk
```

```
> ipython
...
In [1]: import nltk
In [2]: nltk.__version__
Out[2]: '3.4.5'
```

NLTK의 기능을 제대로 사용하기 위해서는 NLTK Data라는 여러 데이터를 추가적으로 설치해야 한다. 이를 위해서는 파이썬 코드 내에서 import nltk 이후에 nltk.download()라는 코드를 수행하여 설치한다.

```
In [3]: nltk.download()
```

#### 2) KoNLPy 설치

코엔엘파이(KoNLPy)는 한국어 자연어 처리를 위한 형태소 분석기 패키지다. 프롬프트에서 아래 커맨드로 설치한다.

```
> pip install konlpy
```

```
> ipython
...
In [1]: import konlpy
In [2]: konlpy.__version__
Out[2]: '0.5.1'
```

