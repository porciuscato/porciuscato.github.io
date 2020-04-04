# 딥러닝을 위한 자연어 처리 입문

[위키독스](https://wikidocs.net/22488)

## 텍스트 전처리(Text Preprocessing)

자연어 처리에 있어서 텍스트 전처리는 매우 중요한 작업이다. 텍스트 전처리는 용도에 맞게 텍스트를 사전에 처리하는 작업이다. 텍스트에 대해서 제대로 된 전처리를 하지 않으면 자연어 처리 기법들이 제대로 동작하지 않는다.

#### 차례

1) [토큰화(Tokenization)](#토큰화(Tokenization))

2) [정제(Cleaning) and 정규화(Normalization)](#정제(Cleaning) and 정규화(Normalization))

3) [어간 추출(Stemming) and 표제어 추출(Lemmatization)](#어간 추출(Stemming) and 표제어 추출(Lemmatization))

4) [불용어(Stopword)](#불용어(Stopword))

5) [정규 표현식(Regular Expression)](#정규 표현식(Regular Expression))

6) [정수 인코딩(Integer Encoding)](#정수 인코딩(Integer Encoding))

7) [원-핫 인코딩(One-hot encoding)](#원-핫 인코딩(One-hot encoding))

8) [단어 분리하기(Byte Pair Encoding, BPE)](#단어 분리하기(Byte Pair Encoding, BPE))

9) [데이터의 분리(Splitting Data)](#데이터의 분리(Splitting Data))



## 토큰화(Tokenization)

자연어 처리에서 크롤링 등으로 얻어낸 코퍼스 데이터가 필요에 맞게 전처리되지 않은 상태라면, 해당 데이터를 사용하고자하는 용도에 맞게 토큰화(tokenization) & 정제(cleaning) & 정규화(normalization)하는 일을 하게 된다. 그 중에서도 토큰화에 대해서 다뤄보자.

주어진 코퍼스(corpus)에서 토큰(token)이라 불리는 단위로 나누는 작업을 토큰화(tokenization)라고 부른다. 토큰의 단위가 상황에 따라 다르지만, 보통 의미있는 단위로 토큰을 정의한다.

### 1. 단어 토큰화 Word Tokenization

토큰의 기준을 단어(word)로 하는 경우, 단어 토큰화(word tokenization)라고 한다. 다만, 여기서 단어(word)는 단어 단위 외에도 단어구, 의미를 갖는 문자열로도 간주되기도 한다.

예를 들어, 아래의 입력으로부터 구두점(punctuation)과 같은 문자는 제외시키는 간단한 단어 토큰화 작업을 해보자. 구두점이란, 온점(.), 컴마(,), 물음표(?), 세미콜론(;), 느낌표(!) 등과 같은 기호다.

```
입력: Time is an illusion. Lunchtime double so!
```

이러한 입력으로부터 구두점을 제외시킨 토큰화 작업의 결과는 다음과 같다.

```
출력 : "Time", "is", "an", "illustion", "Lunchtime", "double", "so"
```

보통 토큰화 작업은 단순히 구두점이나 특수문자를 전부 제거하는 정제(cleaning) 작업을 수행하는 것만으로 해결되지 않는다. 구두점이나 특수문자를 전부 제거하면 토큰이 의미를 잃어버리는 경우가 발생하기도 한다. 심지어 띄어쓰기 단위로 자르면 사실상 단어 토큰이 구분되는 영어와 달리, 한국어는 띄어쓰기만으로는 단어 토큰을 구분하기 어렵다. 

### 2. 토큰화 중 생기는 선택의 순간

토큰화 중, 예상하지 못한 경우가 있어 토큰화의 기준을 생각해봐야 하는 경우가 발생한다. 물론, 이러한 선택은 해당 데이터를 가지고 어떤 용도로 사용할 것인지에 따라, 그 용도에 영향이 없는 기준으로 정하면 된다. 예를 들어 영어권 언어에서 아포스트로피를(')가 들어가있는 단어는 어떻게 토큰으로 분류해야할까라는 문제를 고려해보자.

예를 들어

```
Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop.
```

`'`가 들어갔을 때 Don't와 Jone's는 어떻게 토큰화할 수 있을까?

- Don't / Don t / Dont / Do n't
- Jone's / Jone s / Jone / Jones

원하는 결과가 나오도록 토큰화 도구를 직접 설계할 수도 있겠지만, 기존에 공개된 도구들을 사용하였을 때의 결과가 사용자의 목적과 일치한다면 해당 도구를 사용할 수도 있다. NLTK는 영어 코퍼스를 토큰화하기 위한 도구들을 제공한다. 그 중 word_tokenize와 WordPunctTokenizer를 사용해서 NLTK에서는 아포스트로피를 어떻게 처리하는지 확인해보겠습니다.

#### NLTK word_tokenize

```python
from nltk.tokenize import word_tokenize  
print(word_tokenize("Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop.")) 
```

```python
['Do', "n't", 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'name', ',', 'Mr.', 'Jone', "'s", 'Orphanage', 'is', 'as', 'cheery', 'as', 'cheery', 'goes', 'for', 'a', 'pastry', 'shop', '.']  
```

word_tokenize는 Don't를 Do와 n't로 분리하였으며, 반면 Jone's는 Jone과 's로 분리한 것을 확인할 수 있다.

 #### NLTK WordPuctTokenizer

```python
from nltk.tokenize import WordPunctTokenizer  
print(WordPunctTokenizer().tokenize("Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop."))
```

```python
['Don', "'", 't', 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'name', ',', 'Mr', '.', 'Jone', "'", 's', 'Orphanage', 'is', 'as', 'cheery', 'as', 'cheery', 'goes', 'for', 'a', 'pastry', 'shop', '.']  
```

WordPunctTokenizer는 구두점을 별도로 분류하는 특징을 갖고 있기때문에, 앞서 확인했던 word_tokenize와는 달리 Don't를 Don과 '와 t로 분리하였으며, 이와 마찬가지로 Jone's를 Jone과 '와 s로 분리한 것을 확인할 수 있다.

#### keras

```python
from tensorflow.keras.preprocessing.text import text_to_word_sequence
print(text_to_word_sequence("Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop."))
```

```python
["don't", 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'name', 'mr', "jone's", 'orphanage', 'is', 'as', 'cheery', 'as', 'cheery', 'goes', 'for', 'a', 'pastry', 'shop']
```

케라스의 text_to_word_sequence는 기본적으로 모든 알파벳을 소문자로 바꾸면서 온점이나 컴마, 느낌표 등의 구두점을 제거한다. 하지만 don't나 jone's와 같은 경우 아포스트로피는 보존하는 것을 볼 수 있다.

### 3. 토큰화에서 고려해야할 사항

토큰화 작업을 단순하게 코퍼스에서 구두점을 제외하고 공백 기준으로 잘라내는 작업이라고 간주할 수는 없다. 이러한 일은 보다 섬세한 알고리즘이 필요한데, 왜 섬세해야하는지 지금부터 그 이유를 정리해보자.

#### 1) 구두점이나 특수 문자를 단순 제외해서는 안 된다.

구두점이나 특수 문자를 단순히 제외하는 것은 옳지 않다. 정제 작업 중, 구두점조차도 하나의 토큰으로 분류될 수 있다. 예를 들어, 온점(.)의 경우는 문장의 경계를 알려 주므로 단어를 뽑아낼 때, 온점(.)을 제외하지 않을 수 있다.

또 다른 예로, 단어 자체에서 구두점을 갖고 있는 경우도 있는데, m.p.h나 Ph.D나 AT&T 같은 경우가 있다. 또 특수 문자의 달러(![img](https://wikidocs.net/images/page/21693/%EB%8B%AC%EB%9F%AC.PNG))나 슬래시(/)로 예를 들어보면, $45.55와 같은 가격, 01/02/06은 날짜를 의미한다. 보통 이런 경우 45.55를 하나로 취급해야하지, 45와 55로 따로 분류해서는 안 된다.

숫자 사이에 컴마(,)가 들어가는 경우도 있다. 가령 보통 수치를 표현할 때는 123,456,789와 같이 세 자리 단위로 컴마가 들어간다.

#### 2) 줄임말과 단어 내에 띄어쓰기가 있는 경우

토큰화 작업에서 종종 영어권 언어의 아포스트로피(')는 압축된 단어를 다시 펼치는 역할도 한다. 예를 들어 what're는 what are의 줄임말이며, we're는 we are의 줄임말입니다. 위의 예에서 re를 접어(clitic)이라고 한다. 즉, 단어가 줄임말로 쓰일 때 생기는 형태를 말한다. 가령 I am을 줄인 I'm이 있을 때, m을 접어라고 한다.

New York이라는 단어나 rock 'n' roll이라는 단어를 봅시다. 이 단어들은 하나의 단어이지만 중간에 띄어쓰기가 존재한다. 사용 용도에 따라서, 하나의 단어 사이에 띄어쓰기가 있는 경우에도 하나의 토큰으로 봐야하는 경우도 있을 수 있으므로, 토큰화 작업은 저러한 단어를 하나로 인식할 수 있는 능력도 가져야한다.

#### 3) 표준 토큰화 예제

이해를 돕기 위해, 표준으로 쓰이고 있는 토큰화 방법 중 하나인 Penn Treebank Tokenization의 규칙에 대해서 소개하고, 토큰화의 결과를 살펴 보자.

- 규칙 1. 하이푼으로 구성된 단어는 하나로 유지한다.
- 규칙 2. doesn't와 같이 아포스트로피로 '접어'가 함께하는 단어는 분리해준다.

해당 표준에 아래의 문장을 input으로 넣어보자.

```python
from nltk.tokenize import TreebankWordTokenizer
tokenizer=TreebankWordTokenizer()
text="Starting a home-based restaurant may be an ideal. it doesn't have a food chain or restaurant of their own."
print(tokenizer.tokenize(text))
```

```python
['Starting', 'a', 'home-based', 'restaurant', 'may', 'be', 'an', 'ideal.', 'it', 'does', "n't", 'have', 'a', 'food', 'chain', 'or', 'restaurant', 'of', 'their', 'own', '.'] 
```

결과를 보면, 각각 규칙1과 규칙2에 따라서 home-based는 하나의 토큰으로 취급하고 있으며, dosen't의 경우 does와 n't는 분리되었음을 볼 수 있다.

### 4. 문장 토큰화 Sentence Tokenization

이번에는 토큰의 단위가 문장(sentence)일 때, 어떻게 토큰화를 수행해야할지 논의해보도록 하자. 이 작업은 갖고있는 코퍼스 내에서 문장 단위로 구분하는 작업으로 때로는 문장 분류(sentence segmentation)라고도 불린다.

보통 갖고있는 코퍼스가 정제되지 않은 상태라면, 코퍼스는 문장 단위로 구분되어있지 않을 가능성이 높다. 이를 사용하고자 하는 용도에 맞게 하기 위해서는 문장 토큰화가 필요할 수 있다.

어떻게 주어진 코퍼스로부터 문장 단위로 분류하는가? ?나 온점(.)이나 ! 기준으로 문장을 잘라내면 되지 않을까라고 생각할 수 있지만, 꼭 그렇지만은 않다. !나 ?는 문장의 구분을 위한 꽤 명확한 구분자(boundary) 역할을 하지만 온점은 그렇지 않기 때문이다. 다시 말해, 온점은 문장의 끝이 아니더라도 등장할 수 있다.

- EX1) IP 192.168.56.31 서버에 들어가서 로그 파일 저장해서 ukairia777@gmail.com로 결과 좀 보내줘. 그러고나서 점심 먹으러 가자.
- EX2) Since I'm actively looking for Ph.D. students, I get the same question a dozen times every year.

사용하는 코퍼스가 어떤 국적의 언어인지, 또는 해당 코퍼스 내에서 특수문자들이 어떻게 사용되고 있는지에 따라서 직접 규칙들을 정의해볼 수 있다. 물론, 100% 정확도를 얻는 일은 쉬운 일이 아니다. 갖고있는 코퍼스 데이터에 오타나, 문장의 구성이 엉망이라면 정해놓은 규칙이 소용이 없을 수 있기 때문이다.

NLTK에서는 영어 문장의 토큰화를 수행하는 sent_tokenize를 지원하고 있다. NLTK를 통해 문장 토큰화를 실습해보고, 문장 토큰화에 대해 이해해보도록 하자.

##### NLTK sent_tokenize

```python
from nltk.tokenize import sent_tokenize
text="His barber kept his word. But keeping such a huge secret to himself was driving him crazy. Finally, the barber went up a mountain and almost to the edge of a cliff. He dug a hole in the midst of some reeds. He looked about, to mae sure no one was near."
print(sent_tokenize(text))
```

```python
['His barber kept his word.', 'But keeping such a huge secret to himself was driving him crazy.', 'Finally, the barber went up a mountain and almost to the edge of a cliff.', 'He dug a hole in the midst of some reeds.', 'He looked about, to mae sure no one was near.']
```

위 코드는 text에 저장된 여러 개의 문장들로부터 문장을 구분하는 코드다. 출력 결과를 보면 성공적으로 모든 문장을 구분해내었음을 볼 수 있다. 그렇다면, 이번에는 언급했던 문장 중간에 온점이 여러번 등장하는 경우에 대해서도 보자.

```python
from nltk.tokenize import sent_tokenize
text="I am actively looking for Ph.D. students. and you are a Ph.D student."
print(sent_tokenize(text))
```

```python
['I am actively looking for Ph.D. students.', 'and you are a Ph.D student.']
```

NLTK는 단순히 온점을 구분자로 하여 문장을 구분하지 않았기 때문에, Ph.D.를 문장 내의 단어로 인식하여 성공적으로 인식하는 것을 볼 수 있다.

물론, 한국어에 대한 문장 토큰화 도구가 존재한다. 한국어에 대한 문장 토큰화 도구가 여럿있지만, 박상길님이 개발한 KSS(Korean Sentence Splitter)를 살펴보자.

```bash
pip install kss
```

> kss는 윈도우 설치를 지원하지 않는다. 실습을 하려면 리눅스 환경 또는 구글 Colab을 권장한다.

KSS를 통해 문장 토큰화를 해보자.

```python
import kss
text='딥 러닝 자연어 처리가 재미있기는 합니다. 그런데 문제는 영어보다 한국어로 할 때 너무 어려워요. 농담아니에요. 이제 해보면 알걸요?'
print(kss.split_sentences(text))
```

```python
['딥 러닝 자연어 처리가 재미있기는 합니다.', '그런데 문제는 영어보다 한국어로 할 때 너무 어려워요.', '농담아니에요.', '이제 해보면 알걸요?']
```







## 정제(Cleaning) and 정규화(Normalization)

## 어간 추출(Stemming) and 표제어 추출(Lemmatization)

## 불용어(Stopword)

## 정규 표현식(Regular Expression)

## 정수 인코딩(Integer Encoding)

## 원-핫 인코딩(One-hot encoding)

## 단어 분리하기(Byte Pair Encoding, BPE)

## 데이터의 분리(Splitting Data)