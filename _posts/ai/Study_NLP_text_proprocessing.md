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

출력 결과는 정상적으로 모든 문장이 분리된 결과를 보여준다.



### 5. 이진 분류기(Binary Classifier)

문장 토큰화에서의 예외 사항을 발생시키는 온점의 처리를 위해서 입력에 따라 두 개의 클래스로 분류하는 이진 분류기(binary classifier)를 사용하기도 한다.

물론, 여기서 말하는 두 개의 클래스는

1. 온점(.)이 단어의 일부분일 경우. 즉, 온점이 약어(abbreivation)로 쓰이는 경우

2. 온점(.)이 정말로 문장의 구분자(boundary)일 경우

이진 분류기는 앞서 언급했듯이, 임의로 정한 여러가지 규칙을 코딩한 함수일 수도 있으며, 머신 러닝을 통해 이진 분류기를 구현하기도 한다.

온점(.)이 어떤 클래스에 속하는지 결정을 위해서는 어떤 온점이 주로 약어(abbreviation)으로 쓰이는 지 알아야한다. 그렇기 때문에, 이진 분류기 구현에서 약어 사전(abbreviation dictionary)이 유용하게 쓰인다. 영어권 언어의 경우에 있어
이 [링크](https://public.oed.com/how-to-use-the-oed/abbreviations/)는 약어 사전의 예라고 볼 수 있다.

이러한 문장 토큰화를 수행하는 오픈 소스로는 NLTK, OpenNLP, 스탠포드 CoreNLP, splitta, LingPipe 등이 있다. 문장 토큰화 규칙을 짤 때, 발생할 수 있는 여러가지 예외사항을 다룬 참고 자료로 이 [링크](https://tech.grammarly.com/blog/posts/How-to-Split-Sentences.html)를 보면 좋다.




### 6. 한국어에서의 토큰화의 어려움

영어는 New York과 같은 합성어나 he's 와 같이 줄임말에 대한 예외처리만 한다면, 띄어쓰기(whitespace)를 기준으로 하는 띄어쓰기 토큰화를 수행해도 단어 토큰화가 잘 작동한다. 거의 대부분의 경우에서 단어 단위로 띄어쓰기가 이루어지기 때문에 띄어쓰기 토큰화와 단어 토큰화가 거의 같기 때문이다.

하지만 한국어는 영어와는 달리 띄어쓰기만으로는 토큰화를 하기에 부족하다. 한국어는 띄어쓰기 단위가 되는 단위를 '어절'이라고 하는데 즉, 어절 토큰화는 한국어 NLP에서 지양되고 있다. 어절 토큰화와 단어 토큰화가 같지 않기 때문이다. 그 근본적인 이유는 한국어가 영어와는 다른 형태를 가지는 언어인 교착어라는 점에서 기인한다. 교착어란 조사, 어미 등을 붙여서 말을 만드는 언어를 말한다.

#### **1) 한국어는 교착어이다.**

예를 들어 보자. 영어와는 달리 한국어에는 조사라는 것이 있다. 예를 들어, 그(he/him)라는 주어나 목적어가 들어간 문장이 있으면 그라는 단어 하나에도 '그가', '그에게', '그를', '그와', '그는'과 같이 다양한 조사가 '그'라는 글자 뒤에 띄어쓰기 없이 바로 붙는다. 자연어 처리를 하다보면 같은 단어임에도 서로 다른 조사가 붙어서 다른 단어로 인식이 되면 자연어 처리가 힘들고 번거로워지는 경우가 많다. 대부분의 한국어 NLP에서 조사는 분리해줄 필요가 있다.

즉, 띄어쓰기 단위가 영어처럼 독립적인 단어라면 띄어쓰기 단위로 토큰화를 하면 되겠지만 한국어는 어절이 독립적인 단어로 구성되는 것이 아니라 조사 등의 무언가가 붙어있는 경우가 많아서 이를 전부 분리해줘야 한다는 의미다.

한국어 토큰화에서는 **형태소(morpheme)**란 개념을 반드시 이해해야 한다. 형태소(morpheme)란 뜻을 가진 가장 작은 말의 단위를 말한다. 이 형태소에는 두 가지 형태소가 있는데 자립 형태소와 의존 형태소다.

- **자립 형태소** : 접사, 어미, 조사와 상관없이 자립하여 사용할 수 있는 형태소. 그 자체로 단어가 된다. 체언(명사, 대명사, 수사), 수식언(관형사, 부사), 감탄사 등이 있다.

- **의존 형태소** : 다른 형태소와 결합하여 사용되는 형태소. 접사, 어미, 조사, 어간를 말한다.

예를 들어 다음과 같은 문장이 있다고 하자.

- 문장 : 에디가 딥러닝책을 읽었다.

이를 형태소 단위로 분해하면 다음과 같다.

```
자립 형태소 : 에디, 딥러닝책
의존 형태소 : -가, -을, 읽-, -었, -다
```

이를 통해 유추할 수 있는 것은 한국어에서 영어에서의 단어 토큰화와 유사한 형태를 얻으려면 어절 토큰화가 아니라 형태소 토큰화를 수행해야한다는 것이다.

#### **2) 한국어는 띄어쓰기가 영어보다 잘 지켜지지 않는다.**

사용하는 한국어 코퍼스가 뉴스 기사와 같이 띄어쓰기를 철저하게 지키려고 노력하는 글이라면 좋겠지만, 많은 경우에 띄어쓰기가 틀렸거나, 지켜지지 않는 코퍼스가 많다.

한국어는 영어권 언어와 비교하여 띄어쓰기가 어렵고, 또 잘 지켜지지 않는 경향이 있다. 그 이유는 여러 견해가 있으나, 가장 기본적인 견해는 한국어의 경우 띄어쓰기가 지켜지지 않아도 글을 쉽게 이해할 수 있는 언어라는 점이다. 사실, 띄어쓰기가 없던 한국어에 띄어쓰기가 보편화된 것도 근대(1933년, 한글맞춤법통일안)의 일이다.

**EX1) 제가이렇게띄어쓰기를전혀하지않고글을썼다고하더라도글을이해할수있습니다.**

**EX2) Tobeornottobethatisthequestion**

반면, 영어의 경우에는 띄어쓰기를 하지 않으면 손쉽게 알아보기 어려운 문장들이 생깁니다. 이는 한국어(모아쓰기 방식)와 영어(풀어쓰기 방식)라는 언어적 특성의 차이에 기인한다. 모아쓰기와 풀어쓰기에 대한 설명은 생략하겠으나, 결론은 한국어는 수많은 코퍼스에서 띄어쓰기가 무시되는 경우가 많아 자연어 처리가 어려워졌다는 것이다.



### 7. 품사 태깅(Part-of-speech tagging)

단어는 표기는 같지만, 품사에 따라서 단어의 의미가 달라지기도 한다. 예를 들어서 영어 단어 'fly'는 동사로는 '날다'라는 의미를 갖지만, 명사로는 '파리'라는 의미를 갖고있다. 한국어도 마찬가지다. '못'이라는 단어는 명사로서는 망치를 사용해서 목재 따위를 고정하는 물건을 의미한다. 하지만 부사로서의 '못'은 '먹는다', '달린다'와 같은 동작 동사를 할 수 없다는 의미로 쓰인다. 즉, 결국 단어의 의미를 제대로 파악하기 위해서는 해당 단어가 어떤 품사로 쓰였는지 보는 것이 주요 지표가 될 수도 있다. 그에 따라 단어 토큰화 과정에서 각 단어가 어떤 품사로 쓰였는지를 구분해놓기도 하는데, 이 작업을 품사 태깅(part-of-speech tagging)이라고 한다. NLTK와 KoNLPy에서는 어떻게 품사 태깅이 되는지 알아보자.



### 8. NLTK와 KoNLPy를 이용한 영어, 한국어 토큰화 실습

NLTK에서는 영어 코퍼스에 품사 태깅 기능을 지원하고 있다. 품사를 어떻게 명명하고, 태깅하는지의 기준은 여러가지가 있는데, NLTK에서는 Penn Treebank POS Tags라는 기준을 사용한다. 실제로 NLTK를 사용해서 영어 코퍼스에 품사 태깅을 해보도록 하자.

```python
######### 필요한 패키지 설치
import os
os.system('pip install nltk')
import nltk
nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
```

```python
from nltk.tokenize import word_tokenize
text="I am actively looking for Ph.D. students. and you are a Ph.D. student."
print(word_tokenize(text))
'''
['I', 'am', 'actively', 'looking', 'for', 'Ph.D.', 'students', '.', 'and', 'you', 'are', 'a', 'Ph.D.', 'student', '.']
'''
```

```python
from nltk.tag import pos_tag
x=word_tokenize(text)
print(pos_tag(x))
'''
[('I', 'PRP'), ('am', 'VBP'), ('actively', 'RB'), ('looking', 'VBG'), ('for', 'IN'), ('Ph.D.', 'NNP'), ('students', 'NNS'), ('.', '.'), ('and', 'CC'), ('you', 'PRP'), ('are', 'VBP'), ('a', 'DT'), ('Ph.D.', 'NNP'), ('student', 'NN'), ('.', '.')]
'''
```

영어 문장에 대해서 토큰화를 수행하고, 이어서 품사 태깅을 수행했다. Penn Treebank POG Tags에서 PRP는 인칭 대명사, VBP는 동사, RB는 부사, VBG는 현재부사, IN은 전치사, NNP는 고유 명사, NNS는 복수형 명사, CC는 접속사, DT는 관사를 의미한다.

한국어 자연어 처리를 위해서는 KoNLPy("코엔엘파이")라는 파이썬 패키지를 사용할 수 있다. 코엔엘파이를 통해서 사용할 수 있는 형태소 분석기로 **Okt(Open Korea Text), 메캅(Mecab), 코모란(Komoran), 한나눔(Hannanum), 꼬꼬마(Kkma)**가 있다.

한국어 NLP에서 형태소 분석기를 사용한다는 것은 단어 토큰화가 아니라 정확히는 형태소(morpheme) 단위로 형태소 토큰화(morpheme tokenization)를 수행하게 됨을 뜻한다. 여기선 이 중에서 Okt와 꼬꼬마를 통해서 토큰화를 수행해보도록 하겠다. (Okt는 기존에는 Twitter라는 이름을 갖고있었으나 0.5.0 버전부터 이름이 변경되어 인터넷에는 아직 Twitter로 많이 알려져있다.)

##### Okt 

```python
# os.system('pip install konlpy')  # 설치가 안되어 있다면
from konlpy.tag import Okt  
okt=Okt()
text = "열심히 코딩한 당신, 연휴에는 여행을 가봐요"
```

```python
print(okt.morphs(text))
'''
['열심히', '코딩', '한', '당신', ',', '연휴', '에는', '여행', '을', '가봐요'] 
'''
```

```python
print(okt.pos(text))
'''
[('열심히', 'Adverb'), ('코딩', 'Noun'), ('한', 'Josa'), ('당신', 'Noun'), (',', 'Punctuation'), ('연휴', 'Noun'), ('에는', 'Josa'), ('여행', 'Noun'), ('을', 'Josa'), ('가봐요', 'Verb')]
'''
```

```python
print(okt.nouns(text))  
'''
['코딩', '당신', '연휴', '여행'] 
'''
```

위의 예제는 Okt 형태소 분석기로 토큰화를 시도해본 예다.

1) morphs : 형태소 추출

2) pos : 품사 태깅(Part-of-speech tagging)

3) nouns : 명사 추출

위 예제에서 사용된 각 메소드는 이런 기능을 갖고 있다. 앞서 언급한 코엔엘파이의 형태소 분석기들은 공통적으로 이 메소드들을 제공하고 있다. 위 예제에서 형태소 추출과 품사 태깅 메소드의 결과를 보면, 조사를 기본적으로 분리하고 있음을 확인할 수 있다. 그렇기 때문에 한국어 NLP에서 전처리에 형태소 분석기를 사용하는 것은 꽤 유용하다.

이번에는 꼬꼬마 형태소 분석기를 사용하여 같은 문장에 대해서 토큰화를 진행해보자.

```python
from konlpy.tag import Kkma  
kkma=Kkma()  
```

```python
print(kkma.morphs(text))
'''
['열심히', '코딩', '하', 'ㄴ', '당신', ',', '연휴', '에', '는', '여행', '을', '가보', '아요'] 
'''
```

```python
print(kkma.pos(text))
'''
[('열심히','MAG'), ('코딩', 'NNG'), ('하', 'XSV'), ('ㄴ', 'ETD'), ('당신', 'NP'), (',', 'SP'), ('연휴', 'NNG'), ('에', 'JKM'), ('는', 'JX'), ('여행', 'NNG'), ('을', 'JKO'), ('가보', 'VV'), ('아요', 'EFN')]  
'''
```

```python
print(kkma.nouns("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))  
'''
['코딩', '당신', '연휴', '여행']  
'''
```

앞서 사용한 Okt 형태소 분석기와 결과가 다른 것을 볼 수 있다. 각 형태소 분석기는 성능과 결과가 다르게 나오기 때문에, 형태소 분석기의 선택은 사용하고자 하는 필요 용도에 어떤 형태소 분석기가 가장 적절한지를 판단하고 사용하면 된다. 예를 들어서 속도를 중시한다면 메캅을 사용할 수 있다.

---

한국어 형태소 분석기 성능 비교 : [링크](https://iostream.tistory.com/144
http://www.engear.net/wp/%ED%95%9C%EA%B8%80-%ED%98%95%ED%83%9C%EC%86%8C-%EB%B6%84%EC%84%9D%EA%B8%B0-%EB%B9%84%EA%B5%90/)

윈도우10 메캅 설치 :
[링크](https://cleancode-ws.tistory.com/97)



## 정제(Cleaning) and 정규화(Normalization)

코퍼스에서 용도에 맞게 토큰을 분류하는 작업을 토큰화(tokenization)라고 하며, 토큰화 작업 전, 후에는 텍스트 데이터를 용도에 맞게 정제(cleaning) 및 정규화(normalization)하는 일이 항상 함께 한다. 정제 및 정규화의 목적은 각각 다음과 같다.

- 정제(cleaning) : 갖고 있는 코퍼스로부터 노이즈 데이터를 제거한다.
- 정규화(normalization) : 표현 방법이 다른 단어들을 통합시켜서 같은 단어로 만들어준다.

정제 작업은 토큰화 작업에 방해가 되는 부분들을 배제시키고 토큰화 작업을 수행하기 위해서 토큰화 작업보다 앞서 이루어지기도 하지만, 토큰화 작업 이후에도 여전히 남아있는 노이즈들을 제거하기위해 지속적으로 이루어지기도 한다. 사실 완벽한 정제 작업은 어려운 편이라서, 대부분의 경우 '이 정도면 됐다'라는 일종의 합의점을 찾기도 한다. 

이번엔 정제와 정규화 기법에 대해 다루자.

### 1. 규칙에 기반한 표기가 다른 단어들의 통합

필요에 따라 직접 코딩을 통해 정의할 수 있는 정규화 규칙의 예로서 같은 의미를 갖고있음에도, 표기가 다른 단어들을 하나의 단어로 정규화하는 방법을 사용할 수 있다.

가령, USA와 US는 같은 의미를 가지므로, 하나의 단어로 정규화해볼 수 있다. uh-huh와 uhhuh는 형태는 다르지만 여전히 같은 의미를 갖고 있습니다. 이러한 정규화를 거치게 되면, US를 찾아도 USA도 함께 찾을 수 있다. 다음에 표기가 다른 단어들을 통합하는 방법인 어간 추출(stemming)과 표제어 추출(lemmatizaiton)에 대해서 더 자세히 알아보도록 하자.

### 2. 대, 소문자 통합

영어권 언어에서 대, 소문자를 통합하는 것은 단어의 개수를 줄일 수 있는 또 다른 정규화 방법이다. 영어권 언어에서 대문자는 문장의 맨 앞 등과 같은 특정 상황에서만 쓰이고, 대부분의 글은 소문자로 작성되기 때문에 대, 소문자 통합 작업은 대부분 대문자를 소문자로 변환하는 소문자 변환작업으로 이루어지게 된다.

소문자 변환이 왜 유용한지 예를 들어보자. 가령, Automobile이라는 단어가 문장의 첫 단어였기때문에 A가 대문자였다고 생각해보자. 여기에 소문자 변환을 사용하면, automobile을 찾는 질의(query)에서, 결과로서 Automobile도 찾을 수 있게 된다.

유사하게, 검색 엔진에서 사용자가 페라리 차량에 관심이 있어서 페라리를 검색해본다고 하자. 엄밀히 말해서 사실 사용자가 검색을 통해 찾고자하는 결과는 a Ferrari car라고 봐야한다. 하지만, 검색 엔진은 소문자 변환을 적용했을 것이기 때문에 ferrari만 쳐도 원하는 결과를 얻을 수 있을 것이다.

물론, 대문자와 소문자를 무작정 통합해서는 안 된다. 대문자와 소문자가 구분되어야 하는 경우도 있기 때문입니다. 가령 미국을 뜻하는 단어 US와 우리를 뜻하는 us는 구분되어야 한다. 또 회사 이름(General Motors)나, 사람 이름(Bush) 등은 대문자로 유지되는 것이 옳다.

모든 토큰을 소문자로 만드는 것이 문제를 가져온다면, 또 다른 대안은 일부만 소문자로 변환시키는 방법도 있다. 가령, 이런 규칙은 어떤가? 문장의 맨 앞에서 나오는 단어의 대문자만 소문자로 바꾸고, 다른 단어들은 전부 대문자인 상태로 놔두는 것이다.

사실, 이러한 작업은 더 많은 변수를 사용해서 소문자 변환을 언제 사용할지 결정하는 머신 러닝 시퀀스 모델로 더 정확하게 진행시킬 수 있다. 하지만 만약 올바른 대문자 단어를 얻고 싶은 상황에서, 훈련에 사용하는 코퍼스가 사용자들이 단어의 대문자, 소문자의 올바른 사용 방법과 상관없이 소문자를 사용하는 사람들로부터 나온 데이터라면 이러한 방법 또한 그다지 도움이 되지 않을 수 있다. 결국에는 예외 사항을 크게 고려하지 않고, 모든 코퍼스를 소문자로 바꾸는 것이 종종 더 실용적인 해결책이 되기도 한다.

### 3. 불필요한 단어의 제거(Removing Unnecessary Words)

정제 작업에서 제거해야하는 노이즈 데이터(noise data)는 자연어가 아니면서 아무 의미도 갖지 않는 글자들(특수 문자 등)을 의미하기도 하지만, 분석하고자 하는 목적에 맞지 않는 불필요 단어들을 노이즈 데이터라고 한다.

불필요 단어들을 제거하는 방법으로는 불용어 제거와 등장 빈도가 적은 단어, 길이가 짧은 단어들을 제거하는 방법이 있다. 불용어 제거는 불용어 챕터에서 더욱 자세히 다루기로 하고, 여기서는 등장 빈도가 적은 단어와 길이가 짧은 단어를 제거하는 경우에 대해서 보자.

#### (1) 등장 빈도가 적은 단어(Removing Rare words)

때론 텍스트 데이터에서 너무 적게 등장해서 자연어 처리에 도움이 되지 않는 단어들이 존재한다. 예를 들어 입력된 메일이 정상 메일인지 스팸 메일인지를 분류하는 스팸 메일 분류기를 설계한다고 가정해보자. 총 100,000개의 메일을 가지고 정상 메일에서는 어떤 단어들이 주로 등장하고, 스팸 메일에서는 어떤 단어들이 주로 등장하는지를 가지고 설계하고자 한다. 그런데 이때 100,000개의 메일 데이터에서 총 합 5번 밖에 등장하지 않은 단어가 있다면 이 단어는 직관적으로 분류에 거의 도움이 되지 않을 것임을 알 수 있다.

#### (2) 길이가 짧은 단어(Removing words with very a short length)

영어권 언어에서는 길이가 짧은 단어를 삭제하는 것만으로도 어느정도 자연어 처리에서 크게 의미가 없는 단어들을 제거하는 효과를 볼 수 있다고 알려져 있다. 즉, 영어권 언어에서 길이가 짧은 단어들은 대부분 불용어에 해당된다. 사실 길이가 짧은 단어를 제거하는 2차 이유는 길이를 조건으로 텍스트를 삭제하면서 단어가 아닌 구두점들까지도 한꺼번에 제거하기 위함도 있다. 하지만 한국어에서는 길이가 짧은 단어라고 삭제하는 이런 방법이 크게 유효하지 않을 수 있는데 그 이유에 대해서 살펴보자.

단정적으로 말할 수는 없지만, 영어 단어의 평균 길이는 6~7 정도이며, 한국어 단어의 평균 길이는 2~3 정도로 추정되고 있다. 두 나라의 단어 평균 길이가 몇 인지에 대해서는 확실히 말하기 어렵지만 그럼에도 확실한 사실은 영어 단어의 길이가 한국어 단어의 길이보다는 평균적으로 길다는 점이다.

이는 영어 단어와 한국어 단어에서 각 한 글자가 가진 의미의 크기가 다르다는 점에서 기인한다. 한국어 단어는 한자어가 많고, 한 글자만으로도 이미 의미를 가진 경우가 많다. 예를 들어 '학교'라는 한국어 단어를 생각해보면, 배울 학(學)과 학교 교(校)로 글자 하나, 하나가 이미 함축적인 의미를 갖고있어 두 글자만으로 학교라는 단어를 표현한다. 하지만 영어의 경우에는 학교라는 글자를 표현하기 위해서는 s, c, h, o, o, l이라는 총 6개의 글자가 필요하다. 다른 예로는 전설 속 동물인 용(龍)을 표현하기 위해서는 한국어로는 한 글자면 충분하지만, 영어에서는 d, r, a, g, o, n이라는 총 6개의 글자가 필요합니다.

이러한 특성으로 인해 영어는 길이가 2~3 이하인 단어를 제거하는 것만으로도 크게 의미를 갖지 못하는 단어를 줄이는 효과를 갖고있다. 예를 들어 갖고 있는 텍스트 데이터에서 길이가 1인 단어를 제거하는 코드를 수행하면 대부분의 자연어 처리에서 의미를 갖지 못하는 단어인 관사 'a'와 주어로 쓰이는 'I'가 제거된다. 마찬가지로 길이가 2인 단어를 제거한다고 하면 it, at, to, on, in, by 등과 같은 대부분 불용어에 해당되는 단어들이 제거된다. 필요에 따라서는 길이가 3인 단어도 제거할 수 있지만, 이 경우 fox, dog, car 등 길이가 3인 명사들이 제거 되기시작하므로 사용하고자 하는 데이터에서 해당 방법을 사용해도 되는지에 대한 고민이 필요하다.

```python
# 길이가 1~2인 단어들을 정규 표현식을 이용하여 삭제
import re
text = "I was wondering if anyone out there could enlighten me on this car."
shortword = re.compile(r'\W*\b\w{1,2}\b')
```

```python
print(shortword.sub('', text))
'''
 was wondering anyone out there could enlighten this car.
'''
```

### 4. 정규 표현식(Regular Expression)

얻어낸 코퍼스에서 노이즈 데이터의 특징을 잡아낼 수 있다면, 정규 표현식을 통해서 이를 제거할 수 있는 경우가 많다. 가령, HTML 문서로부터 가져온 코퍼스라면 문서 여기저기에 HTML 태그가 있다. 뉴스 기사를 크롤링 했다면, 기사마다 게재 시간이 적혀져 있을 수 있다. 정규 표현식은 이러한 코퍼스 내에 계속해서 등장하는 글자들을 규칙에 기반하여 한 번에 제거하는 방식으로서 매우 유용하다.



## 어간 추출(Stemming) and 표제어 추출(Lemmatization)

정규화 기법 중 코퍼스에 있는 단어의 개수를 줄일 수 있는 기법인 표제어 추출(lemmatization)과 어간 추출(stemming)의 개념에 대해서 알아보자. 또한 이 둘의 결과가 어떻게 다른지 이해해보자.

이 두 작업이 갖고 있는 의미는 눈으로 봤을 때는 서로 다른 단어들이지만, 하나의 단어로 일반화시킬 수 있다면 하나의 단어로 일반화시켜서 문서 내의 단어 수를 줄이겠다 것이다. 이러한 방법들은 단어의 빈도수를 기반으로 문제를 풀고자 하는 BoW(Bag of Words) 표현을 사용하는 자연어 처리 문제에서 주로 사용된다. BoW 표현은 뒤에 나온다. 자연어 처리에서 전처리, 더 정확히는 정규화의 지향점은 언제나 갖고 있는 코퍼스로부터 복잡성을 줄이는 일이다.





www.jobis.co







## 불용어(Stopword)

## 정규 표현식(Regular Expression)

## 정수 인코딩(Integer Encoding)

## 원-핫 인코딩(One-hot encoding)

## 단어 분리하기(Byte Pair Encoding, BPE)

## 데이터의 분리(Splitting Data)