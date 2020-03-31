참고: [링크](https://excelsior-cjh.tistory.com/183?category=940400)

../.. -> 빈칸으로 바꾸자

\+ 모두를 위한 딥러닝 [link](https://hunkim.github.io/ml/)

모두의 딥러닝 이북[link](https://thebook.io/006958/part05/ch17/01-02/) 

# 순환 신경망(RNN, Recurrent Neural Network)

CNN이 이미지 데이터에 적합한 모델인 반면 RNN은 자연어(NL, Natural language)나 음성신호, 주식과 같은 연속적인(sequential) 시계열(time series) 데이터에 적합한 모델이다.



## 1. 순환 뉴런(Recurrent Neurons)

피드포워드 신경망이란 입력층 -> 출력층 한 방향으로만 흐르는 신경망을 일컫는다. RNN(순환 신경망)은 피드포워드 신경망과 비슷하지만, 출력을 다시 입력으로 받는 부분이 있다.

<center><img src="../../assets/images/AI/rnn_input.png" width="30%" style="margin: 0px auto;"></center>

RNN은 입력(x)을 받아 출력(y)을 만들고, 이 출력을 다시 입력으로 받는다. 일반적으로 RNN을 그림으로 나타내면 위처럼 하나가 아닌 아래처럼 타임 스텝(time step) $t$  마다 순환 뉴런을 펼처서 타임스텝 별 입력($x_t$)과 출력($y_t$)을 나타낸다. 

<center><img src="../../assets/images/AI/rnn_timestep.png" width="100%" style="margin: 0px auto;"></center>

순환 뉴런으로 구성된 층(layer)은 아래의 그림처럼 나타낼 수 있는데, 타임 스텝 $t$ 마다 모든 뉴런은 입력 벡터 $x_t$와 이전 타임 스텝의 출력 벡터 $y_{t-1}$을 입력받는다. 

<center><img src="../../assets/images/AI/rnn_neurons.png" width="100%" style="margin: 0px auto;"></center>

각 순환 뉴런은 두 개의 가중치 $w_x$ 와 $w_y$를 가지는데, $w_x$ 는 $x_t$를 위한 것이고 $w_y$는 이전 타임 스텝의 출력 $y_{t-1}$을 위한 것이다. 이것을 순환 층(layer) 전체로 생각하면 가중치 벡터 $w_x$와 $w_y$를 행렬 $W_x$와 $W_y$로 나타낼 수 있으며 다음의 식과 같이 표현할 수 있다.
$$
\begin{align*}
y_t = \phi(W_x^T)\cdot x_t + W_y^T\cdot y_{t-1}+b
\end{align*}
$$
그리고 타임 스텝 $t$에서의 미니배치(mini-batch)의 입력을 행렬 $X_t$로 나타내어 아래와 같이 순환 층의 출력을 한 번에 계산할 수 있다.
$$
\begin{align*}
Y_t &= \phi(X_t\cdot W_x + Y_{t-1}\cdot W_y + b) \\
&= \phi(\begin{bmatrix}X_t & Y_{t-1}\end{bmatrix}\begin{bmatrix}W_x\\W_y \end{bmatrix} + b)
\end{align*}
$$

- $Y_t$: 타임 스텝 $t$에서 미니배치에 있는 각 샘플(미니배치)에 대한 순환 층의 출력이며, $m\times n_{neurons}$ 행렬($m$은 미니배치, $n_neurons$은 뉴런 수)

- $X_t$: 모든 샘플의 입력값을 담고 있는 $m\times n_{inputs}$ 행렬($n_{inputs}$은 입력 특성 수)
- $W_x$: 현재 타임 스텝 $t$의 입력에 대한 가중치를 담고 있는 $n_{inputs}\times n_{neurons}$ 행렬
- $W_y$: 이전 타임 스텝 $t_1$의 출력에 대한 가중치를 담고 있는 $n_{neurons}\times n_{neurons}$ 행렬 
- $b$: 각 뉴런의 편향(bias)를 담고 있는 $n_{neurons}$ 크기의 벡터

위의 식에서 $Y_t$는 $X_t$와 $Y_{t-1}$의 함수이므로, 타임 스텝 $t=0$에서부터 모든 입력에 대한 함수가 된다. 첫 번째 타임 스텝인 $t=0$에서는 이전의 출력이 없기 때문에 일반적으로 0으로 초기화 된다.



### 1.1 메모리 셀

타임 스텝 $t$에서 순환 뉴런의 출력은 이전 타임 스텝의 모든 입력에 대한 함수이기 때문에 이것을 **메모리**라고 볼 수 있다. 이렇게 타임 스텝에 걸쳐 어떠한 상태를 보존하는 신경망의 구성 요소를 **메모리 셀**(memory cell) 또는 셀(cell)이라 한다. 일반적으로 타임 스텝 $t$에서 셀의 상태 $h_t$(h=hidden)는 아래의 식과 같이 타임 스텝에서의 입력과 이전 타임 스텝의 상태에 대한 함수이다.
$$
h_t = f(h_{t-1}, x_t)
$$
위에서 살펴본 RNN은 출력 $y_t$가 다시 입력으로 들어갔지만, 아래의 그림과 같이 일반적으로 많이 사용되는 RNN은 출력 $y_t$와 히든 상태(state) $h_t$가 구분되며, 입력으로는 $h_t$가 들어간다. RNN에서의 활성화 함수로는 $tanh$가 주로 사용되는데, 이유는 LSTM을 살펴볼 때 알아보도록 하자.

<center><img src="../../assets/images/AI/rnn_hidden.png" width="100%" style="margin: 0px auto;"></center>

위의 그림을 식으로 나타내면 다음과 같다.
$$
\begin{align*}
h_t &= tanh(X_t\cdot W_x + h_{t-1}\cdot W_h + b) \\
Y_t &= W_y^T\cdot h_t
\end{align*}
$$

### 1.2 입력과 출력 시퀀스 

RNN은 아래의 그림과 같이 다양한 입력 시퀀스를 받아 출력 시퀀스를 만들 수 있다.

<center><img src="../../assets/images/AI/rnn_sequence.png" width="100%" style="margin: 0px auto;"></center>

위의 그림에서 Vector-to-Sequence는 첫 번째 타임 스텝에서 하나의 입력만(다른 모든 타임스텝에서는 0)을 입력받아 시퀀스를 출력하는 네트워크이며, 이러한 모델은 Image Captioning에 사용할 수 있다. Sequence-to-Vector는 Vector-to-Sequence와는 반대로 입력으로 시퀀스를 받아 하나의 벡터를 출력하는 네트워크로, Sentiment Classification에 사용할 수 있다.

위는 그림의 오른쪽에서 세 번째 Sequence-to-Sequence는 시퀀스를 입력받아 시퀀스를 출력하는 네트워크이며, 주식가격과 같은 시게열 데이터를 예측하는 데 사용할 수 있다. 마지막으로 Delayed Sequence-to-Sequence는 인코더(encoder)에는 seq-to-vec 네트워크를 디코더(decoder)에는 vec-to-seq 네트워크를 연결한 것으로, 기계 번역에 사용된다.



## 2. 텐서플로로 기본 RNN 구성하기

위에서 살펴본 RNN을 텐서플로(TensorFlow)를 이용해 구현해보자. 먼저, RNN의 구조를 살펴보기 위해 텐서플로에서 제공하는 RNN을 사용하지 않고 간단한 RNN 모델을 구현해보도록 하자.

아래의 코드는 $tanh$를 활성화 함수로 사용하고, 5개의 뉴런으로 구성된 RNN을 구현하였으며, 타임 스텝마다 크기 3의 입력을 받고 두 개의 타임 스텝($t=0,t=1$)에 대해 작동한다. 

```python
import numpy as np
import tensorflow as tf

n_inputs = 3
n_neurons = 5

X0 = tf.placeholder(tf.float32, [None, n_inputs])
X1 = tf.placeholder(tf.float32, [None, n_inputs])

Wx = tf.Variable(tf.random_normal(shape=[n_inputs, n_neurons], dtype=tf.float32))
Wy = tf.Variable(tf.random_normal(shape=[n_neurons, n_neurons], dtype=tf.float32))
b = tf.Variable(tf.zeros([1, n_neurons], dtype=tf.float32))

Y0 = tf.tanh(tf.matmul(X0, Wx) + b)
Y1 = tf.tanh(tf.matnul(Y0, Wy) + tf.matnul(X1, Wx) + b)

# input data(mini-batch)
# t = 0
X0_batch = np.array([0, 1, 2],
                    [3, 4, 5],
                    [6, 7, 8],
                    [9, 0, 1])
# t = 1
X1_batch = np.array([9, 8, 7],
                    [3, 4, 5],
                    [6, 5, 4],
                    [3, 2, 1])

with tf.Session() as sess:
    tf.global_variables_initializer().run()
    Y0_val, Y1_val = sess.run([Y0, Y1], feed_dict={X0: X0_batch, X1: x1_batch})

print('Y0_val:{}\n{}'.format(Y0_val.shape, Y0_val)) # shape: (4, 5) -> (샘플 개수, 뉴런 개수)
print('Y1_val:{}\n{}'.format(Y1_val.shape, Y1_val))

'''
Y0_val:(4, 5) 
[[-0.0664006 0.9625767 0.68105793 0.7091854 -0.898216 ] 
 [ 0.9977755 -0.719789 -0.9965761 0.9673924 -0.9998972 ] 
 [ 0.99999774 -0.99898803 -0.9999989 0.9967762 -0.9999999 ] 
 [ 1. -1. -1. -0.99818915 0.9995087 ]] 
Y1_val:(4, 5) 
[[ 1. -1. -1. 0.4020025 -0.9999998 ] 
 [-0.12210419 0.62805265 0.9671843 -0.9937122 -0.2583937 ] 
 [ 0.9999983 -0.9999994 -0.9999975 -0.85943305 -0.9999881 ]
 [ 0.99928284 -0.99999815 -0.9999058 0.9857963 -0.92205757]] 
'''
```

위 예제는 2개의 타임 스텝에 대해서만 RNN 연산을 수행했기 때문에 간단해 보였다. 하지만, 타임 스텝이 많아 질수록 연산 그래프가 커지게 된다.

이번에는 텐서플로에서 제공하는 RNN 연산을 사용해 위와 동일한 모델을 만들어 보도록 하자.



### 2.1 정적으로 타임 스텝 펼치기

텐서플로에서 제공하는 RNN 중 `tf.nn.rnn_cell.BasicRNNCell`은 아래의 그림을 그대로 코드로 구현한 것이라고 할 수 있다.

<center><img src="../../assets/images/AI/rnn_cell.png" width="40%" style="margin: 0px auto;"></center>

그런 다음 `tf.nn.static_rnn()` 함수를 호출한 뒤 셀(`BasicRNNCell`)과 입력 텐서, 그리고 입력의 데이터 타입을 알려준다. 기본적으로 모두 0으로 채워진 초기 상태의 행렬을 만든다.

`static_rnn()` 함수는 셀의 `__cell__()` 함수를 호출하여 타임 스텝마다(위의 예제에서는 2개) 셀 복사본을 만들고 서로 연결해준다. 즉, 아래의 그림처럼 하나의 RNN 셀을 타임 스텝별로 펼친 것이라 할 수 있다.

<center><img src="../../assets/images/AI/rnn_cells.png" width="100%" style="margin: 0px auto;"></center>

`static_rnn()` 함수는 출력(output)과 상태(state)를 리턴하는데, 출력은 각 타임 스텝에서의 출력 텐서를 담고 있는 리스트이고 상태는 네트워크의 최종 상태가 담겨 있는 텐서이다. 따라서 최종 상태(state)가 마지막 출력(output)과 동일하다.

아래 코드는 `BasicRNNCell`과 `static_rnn()`을 이용해 위의 예제를 똑같이 구현한 것이다.

```python
import numpy as np 
import tensorflow as tf 

n_inputs = 3 
n_neurons = 5 

X0 = tf.placeholder(tf.float32, [None, n_inputs]) 
X1 = tf.placeholder(tf.float32, [None, n_inputs]) 

# BasicRNNCell 
basic_cell = tf.nn.rnn_cell.BasicRNNCell(num_units=n_neurons) 
# static_rnn() 
output_seqs, states = tf.nn.static_rnn(cell=basic_cell, inputs=[X0, X1], dtype=tf.float32) 

Y0, Y1 = output_seqs 

# input data (mini-batch) 
# t = 0 
X0_batch = np.array([[0, 1, 2], # sample 0 
                     [3, 4, 5], # sample 1 
                     [6, 7, 8], # sample 2 
                     [9, 0, 1]]) # sample 3 
# t = 1 
X1_batch = np.array([[9, 8, 7], 
                     [3, 4, 5], 
                     [6, 5, 4], [3, 2, 1]]) 
with tf.Session() as sess: 
    tf.global_variables_initializer().run() 
    Y0_val, Y1_val = sess.run([Y0, Y1], feed_dict={X0: X0_batch, X1: X1_batch}) 
    
print('Y0_val:{}\n{}'.format(Y0_val.shape, Y0_val)) # shape: (4, 5) → (샘플 개수, 뉴런 개수) 
print('Y1_val:{}\n{}'.format(Y1_val.shape, Y1_val)) 
''' 
Y0_val:(4, 5) 
[[ 0.30741334 -0.32884315 -0.6542847 -0.9385059 0.52089024] 
 [ 0.99122757 -0.9542541 -0.7518079 -0.9995208 0.9820235 ] 
 [ 0.9999268 -0.99783254 -0.8247353 -0.9999963 0.99947774] 
 [ 0.996771 -0.68750614 0.8419969 0.9303911 0.8120684 ]] 
Y1_val:(4, 5) 
[[ 0.99998885 -0.99976057 -0.0667929 -0.9999803 0.99982214] 
 [-0.6524943 -0.51520866 -0.37968948 -0.5922594 -0.08968379] 
 [ 0.99862397 -0.99715203 -0.03308626 -0.9991566 0.9932902 ] 
 [ 0.99681675 -0.9598194 0.39660627 -0.8307606 0.79671973]] 
'''
```



### 하나의 placeholder로 타임 스텝별 데이터 넣어주기

위의 예제에서는 타임 스텝(위의 예제에서는 2개)별 플레이스홀더(placeholder) `X0, X1`를 각각 만들어주고, 2개의 출력 텐서(tensor) `Y0, Y1`를 정의해줬다. 위의 예제에서는 2개의 타임 스탭이어서 괜찮았지만, 만약 타임 스텝이 많아 질수록 타임 스텝별로 플레이스홀더와 출력 텐서를 정의해야하기 때문에 매우 불편하다. 이러한 문제를 해결하기 위해 [미니배치, 타임스텝, 입력크기] 형태인 `[None, n_steps, n_inputs]` 하나의 플레이스홀더 `x`를 만들어주고, 이것을 `tf.unstack()`을 이용해 타임 스텝별로 나누어 준다. 그리고 출력 `outputs`에는 `tf.stack()`을 이용해 모든 출력 텐서들을 하나의 텐서로 합친다. 아래의 예제는 위의 예제를 하나의 플레이스홀더와 출력으로 만든 예제다.

```python
import numpy as np 
import tensorflow as tf 

n_steps = 2 # time steps 
n_inputs = 3 # input size 
n_neurons = 5 

X= tf.placeholder(tf.float32, [None, n_steps, n_inputs]) 
X_seqs = tf.unstack(tf.transpose(X, perm=[1, 0, 2])) 

basic_cell = tf.nn.rnn_cell.BasicRNNCell(num_units=n_neurons) 
output_seqs, states = tf.nn.static_rnn(basic_cell, X_seqs, dtype=tf.float32) 
outputs = tf.transpose(tf.stack(output_seqs), perm=[1, 0, 2]) 

# input data 
X_batch = np.array([
    # t = 0      t = 1 
    [[0, 1, 2], [9, 8, 7]], # 샘플 1 
    [[3, 4, 5], [3, 4, 5]], # 샘플 2 
    [[6, 7, 8], [6, 5, 4]], # 샘플 3 
    [[9, 0, 1], [3, 2, 1]], # 샘플 4 
]) 

with tf.Session() as sess: 
    tf.global_variables_initializer().run() 
    outputs_val = outputs.eval(feed_dict={X: X_batch}) 
    
print('outputs_val:{}\n{}'.format(outputs_val.shape, outputs_val)) 
''' 
outputs_val:(4, 2, 5) 
[[[-0.45652324 -0.68064123 0.40938237 0.63104504 -0.45732826] 
  [-0.9428799 -0.9998869 0.94055814 0.9999985 -0.9999997 ]] 
 
 [[-0.8001535 -0.9921827 0.7817797 0.9971032 -0.9964609 ] 
  [-0.637116 0.11300927 0.5798437 0.4310559 -0.6371699 ]] 
  
 [[-0.93605185 -0.9998379 0.9308867 0.9999815 -0.99998295] 
  [-0.9165386 -0.9945604 0.896054 0.99987197 -0.9999751 ]] 
  
 [[ 0.9927369 -0.9981933 -0.55543643 0.9989031 -0.9953323 ] 
  [-0.02746338 -0.73191994 0.7827872 0.9525682 -0.9781773 ]]] 
'''
```

#### static_rnn()의 문제점

`static_rnn()` 함수의 문제는 타임 스텝마다 하나의 셀을 그래프에 추가하기 때문에, 만약 타입 스텝이 많아질 경우 그래프가 매우 복잡해진다는 것이다. 쉽게 말하면, `for` 문과 같이 반복문을 쓰지 않고 동일한 셀을 타임 스텝별로 만드는 것이라 할 수 있다. 이럴 경우 타임 스텝이 많아서 그래프가 커지게 되면 역전파(backprop)시에 메모리 부족(OOM, Out-of-Memory) 에러가 발생할 수 있다.

이러한 문제를 해결할 수 있는 방법으로는 `tf.nn.dynamic_rnn()`이 있다.