---
comments: true
title: Writing Mathematics on MD. 마크다운에서 수식 작성하기
published: 2020-3-21
updated: 2020-3-21
tags: [markdown, mathmatics]
categories: [development]
---

마크다운에서 수식을 작성하자.



Typora에서 Latex를 사용하면 수학식을 넣을 수 있다. 이를 위해 환경설정에서 Latex 사용을 허가하자.

환경설정 -> Markdown -> 문법 강조 지원 -> `인라인 수식` 을 체크하자.



이 [글](https://csrgxtu.github.io/2015/03/20/Writing-Mathematic-Fomulars-in-Markdown/)을 참조했다.

수식을 작성하려면 먼저 ``$$`` 을 쓰고 엔터를 입력한다. 이는 Math Block을 형성하는 명령어다. 그러면 다음과 같은 창이 뜨는 것을 확인할 수 있다.

```
$$

$$
```

이 안에 식을 작성하면 된다.

가령 $$\alpha$$는 다음과 같은 모양이 된다.
$$
\alpha
$$

여러 줄을 입력하고 싶을 땐 `\\` 을 넣자.
$$
f(x) = \\
\sum_{i=1}^{10}(i^2 + 3i)
$$
위의 소스 코드는 다음과 같다.

```
$$
f(x) = \\
\sum_{i=1}^{10}(i^2 + 3i)
$$
```

위처럼 여러 줄이 아닌, $\alpha$, 이처럼 inline으로 사용하고 싶다면 `$....$` 달러표시를 하나씩 사용하자.





#### Greek letters

| Symbol     | Script   |
| :--------- | :------- |
| $\alpha$   | \alpha   |
| $A$        | A        |
| $\beta$    | \beta    |
| $B$        | B        |
| $\gamma$   | \gamma   |
| $\Gamma$   | \Gamma   |
| $\pi$      | \pi      |
| $\Pi$      | \Pi      |
| $\phi$     | \phi     |
| $\mu$      | \mu      |
| $\sigma$   | \sigma   |
| $\epsilon$ | \epsilon |

$$
\alpha, A, \beta, B, \gamma, \Gamma, \pi, \Pi, \phi, \mu, \sigma, \epsilon
$$

#### Operators

| Symbol   | Script |
| :------- | :----- |
| $\cos$   | \cos   |
| $\sin$   | \sin   |
| $\lim$   | \lim   |
| $\exp$   | \exp   |
| $\to$    | \to    |
| $\infty$ | \infty |
| $\equiv$ | \equiv |
| $\bmod$  | \bmod  |
| $\times$ | \times |

$$
\cos\sin\lim\exp\to\infty\equiv\bmod\times
$$

#### Powers and Indices

| Symbol    | Script  |
| :-------- | :------ |
| $k_{n+1}$ | k_{n+1} |
| $n^2$     | n^2     |
| $k_n^2$   | k_n^2   |

$$
k_{n+1} , n^2 , k_n^2
$$

#### Fractions and Binomials

| Symbol                      | Script                    |
| :-------------------------- | :------------------------ |
| $\frac{n!}{k!(n-k)!}$       | \frac{n!}{k!(n-k)!}       |
| $\binom{n}{k}$              | \binom{n}{k}              |
| $\frac{\frac{x}{1}}{x - y}$ | \frac{\frac{x}{1}}{x - y} |
| $^3/_7$                     | ^3/_7                     |

$$
\frac{n!}{k!(n-k)!}, \binom{n}{k}, \frac{\frac{x}{1}}{x - y}, ^3/_7
$$

#### Roots

| Symbol        | Script      |
| :------------ | :---------- |
| $\sqrt{k}$    | \sqrt{k}    |
| $\sqrt[n]{k}$ | \sqrt[n]{k} |

$$
\sqrt{k}, \sqrt[n]{k}
$$

#### Sums and Integrals

| Symbol                                       | Script                                     |
| :------------------------------------------- | :----------------------------------------- |
| $\sum_{i=1}^{10} t_i$                        | \sum_{i=1}^{10} t_i                        |
| $\int_0^\infty \mathrm{e}^{-x}\,\mathrm{d}x$ | \int_0^\infty \mathrm{e}^{-x}\,\mathrm{d}x |
| $\sum$                                       | \sum                                       |
| $\prod$                                      | \prod                                      |
| $\coprod$                                    | \coprod                                    |
| $\bigoplus$                                  | \bigoplus                                  |
| $\bigotimes$                                 | \bigotimes                                 |
| $\bigodot$                                   | \bigodot                                   |
| $\bigcup$                                    | \bigcup                                    |
| $\bigcap$                                    | \bigcap                                    |
| $\biguplus$                                  | \biguplus                                  |
| $\bigsqcup$                                  | \bigsqcup                                  |
| $\bigvee$                                    | \bigvee                                    |
| $\bigwedge$                                  | \bigwedge                                  |
| $\int$                                       | \int                                       |
| $\oint$                                      | \oint                                      |
| $\iint$                                      | \iint                                      |
| $\iiint$                                     | \iiint                                     |
| $\idotsint$                                  | \idotsint                                  |
| $\sum_{\substack{0<i<m\0<j<n}} P(i, j)$      | \sum_{\substack{0<i<m,0<j<n}} P(i, j)      |
| $\int\limits_a^b$                            | \int\limits_a^b                            |

$$
\sum_{i=1}^{10} t_i, \int_0^\infty \mathrm{e}^{-x}\,\mathrm{d}x, \sum, \prod, \coprod,\\ 
\bigoplus,\bigotimes, \bigodot, \bigcup, \bigcap, \biguplus, \bigsqcup, \bigvee, \bigwedge,\\ 
\int, \oint, \iint, \iiint, \idotsint, \sum_{\substack{0<i<m\0<j<n}} P(i, j), \int\limits_a^b
$$

| Symbol                 | Script               |
| :--------------------- | :------------------- |
| $a’$ $a^{\prime}$      | a` a^{\prime}        |
| $a’’$                  | a’’                  |
| $\hat{a}$              | \hat{a}              |
| $\bar{a}$              | \bar{a}              |
| $\grave{a}$            | \grave{a}            |
| $\acute{a}$            | \acute{a}            |
| $\dot{a}$              | \dot{a}              |
| $\ddot{a}$             | \ddot{a}             |
| $\not{a}$              | \not{a}              |
| $\mathring{a}$         | \mathring{a}         |
| $\overrightarrow{AB}$  | \overrightarrow{AB}  |
| $\overleftarrow{AB}$   | \overleftarrow{AB}   |
| $a’’’$                 | a’’’                 |
| $\overline{aaa}$       | \overline{aaa}       |
| $\check{a}$            | \check{a}            |
| $\vec{a}$              | \vec{a}              |
| $\underline{a}$        | \underline{a}        |
| $\color{red}x$         | \color{red}x         |
| $\pm$                  | \pm                  |
| $\mp$                  | \mp                  |
| $\int y \mathrm{d}x$   | \int y \mathrm{d}x   |
| $!$                    | !                    |
| $\int y\, \mathrm{d}x$ | \int y\, \mathrm{d}x |
| $\dots$                | \dots                |
| $\ldots$               | \ldots               |
| $\cdots$               | \cdots               |
| $\vdots$               | \vdots               |
| $\ddots$               | \ddots               |
| $\propto$ | \propto |
| $\in$ | \in |
| $\cdot$ | $\cdot$ |

$$
a` a^{\prime}, a’’, \hat{a}, \bar{a}, \grave{a}, \acute{a}, \dot{a}, \ddot{a}, \not{a}, \mathring{a},\\ 
\overrightarrow{AB},\overleftarrow{AB}, a’’’, \overline{aaa}, \check{a},\vec{a}, \underline{a}, \color{red}x,\\
\pm,\mp, \int y \mathrm{d}x, !, \int y\, \mathrm{d}x, \\
\dots,\ldots,\cdots, \vdots, \ddots, \propto, \in, \cdot
$$



#### Brackets etc

| Symbol                  | Script                |
| :---------------------- | :-------------------- |
| $(a)$                   | (a)                   |
| $[a]$                   | [a]                   |
| ${a}$                   | {a}                   |
| $\langle f \rangle$     | \langle f \rangle     |
| $\lfloor f \rfloor$     | \lfloor f \rfloor     |
| $\lceil f \rceil$       | \lceil f \rceil       |
| $\ulcorner f \urcorner$ | \ulcorner f \urcorner |

$$
(a),[a], {a}, \langle f \rangle, \lfloor f \rfloor, \lceil f \rceil, \ulcorner f \urcorner
$$

#### Matrix

| Symbol                                     | Script                                     |
| ------------------------------------------ | ------------------------------------------ |
| $\begin{bmatrix}a & b\\c & d\end{bmatrix}$ | `\begin{bmatrix}a & b\\c & d\end{bmatrix}` |
| $\begin{matrix}a & b\\c & d\end{matrix}$   | `\begin{matrix}a & b\\c & d\end{matrix}`   |

$$
\begin{bmatrix}a & b\\c & d\end{bmatrix} \\
\begin{matrix}a & b\\c & d\end{matrix}
$$



#### 예시 - align, 정렬

```
$$
\begin{align*}
y = y(x,t) &= A e^{i\theta} \\
&= A (\cos \theta + i \sin \theta) \\
&= A (\cos(kx - \omega t) + i \sin(kx - \omega t)) \\
&= A\cos(kx - \omega t) + i A\sin(kx - \omega t)  \\
&= A\cos \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big) + i A\sin \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big)  \\
&= A\cos \frac{2\pi}{\lambda} (x - v t) + i A\sin \frac{2\pi}{\lambda} (x - v t)
\end{align*}
$$
```

$$
\begin{align*}
y = y(x,t) &= A e^{i\theta} \\
&= A (\cos \theta + i \sin \theta) \\
&= A (\cos(kx - \omega t) + i \sin(kx - \omega t)) \\
&= A\cos(kx - \omega t) + i A\sin(kx - \omega t)  \\
&= A\cos \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big) + i A\sin \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big)  \\
&= A\cos \frac{2\pi}{\lambda} (x - v t) + i A\sin \frac{2\pi}{\lambda} (x - v t)
\end{align*}
$$