---
layout: post
title:  "Linear Transformation and Matrices"
description: "Dimensions, Change of Basis, Linear transformation, Null spaces, Range spaces, Matrix representations and linear transformations"
category: math
---
* TOC
{:toc}

# 1. Dimensions  
$$ 
(X,F) : \text{vector space} \\  
V=\{v_1, v_2, ... v_n\} \subset X
$$
라고 하자

이때 $X$의 원소들이 $V$의 원소들의 선형결합으로 **유일하게** 표현되면 $V$를 $X$의 basis라고 한다. 또한 이 역도 성립한다.  

$$ 
V \text{ is the basis of X } \\ 
\leftrightarrow x \in X \text{는 } V\text{ 원소들의 선형결합으로 유일하게 표현된다}
$$

**proof**    

1) $\rightarrow$  
   - 가정 : 만일 $V$가 $X$의 basis라면,
    $$
    X=span(V) \rightarrow x=\alpha_1 v_1 + .. +\alpha_n v_n
    $$
  - 만일 유일하지 않다면,  
    $$
    x = \alpha_1 v_1 + ... +\alpha_n v_n = \beta_1 v_1 + ... \beta_n v_n \\
    x-x = 0 = (\alpha_1 \beta_1)v_1 + .... + (\alpha_n - \beta_n)v_n
    $$
  - $ \because V = basis(X) \rightarrow v_i, v_j \text{ : linear independent} $  
    $\therefore a_k - b_k = 0 \rightarrow a_k = b_k $  

1) $\leftarrow$
   - 가정 : $X$ 라는 vector space에서 임의의 $x$를 끌어냈더니, 다음과 같이 표현된다.  
   $$
   x = \alpha_1 v_1 + \alpha_2 v_2 + ... +\alpha_n v_n
   $$  
   - 이는 $span(V) = X$ 라는 뜻


$x = \alpha_1 v_1 + \alpha_2 v_2 + ... + \alpha_n v_n$으로 유일하게 표현되므로 basis를 알고 있다면 그 계수($\alpha_k$)만으로 vector $x$를 표현할 수 있을 것이다. x는 행렬일 수도, 다항식일 수도, 함수일 수도 있지만, 계수는 scalar로 정의되어 있으므로 계수들로 vector를 표현할 수 있다면 다루기 쉬워진다.  

basis가 주어진다면,
 $$\begin{bmatrix}
 \alpha_1 \\
 \alpha_2 \\
 .\\
 .\\
 .\\
 \alpha_n \\
\end{bmatrix}$$ 
처럼 column vector와 동일하게 임의의 vector를 표현할 수 있다.

## Replacement Theorem

$$
(X,F) : \text{vector space}\\
V = \{v_1, v_2, ... , v_n\} \subset X, V \text{ is a basis for X}\\
$$

$$
 U = \{u_1, u_2, ... , u_m\} \subset X, U \text{ is linearly independent} \rightarrow m \leq n 
$$  

**Proof**  
   $m>n$ 이고 U는 선형독립이라고 가정해보자  
   $$V_k := \{u_1, u_2, ... ,u_k,v_{k+1}, ... v_n\} (0 \leq k < n)$$ 가정해보자  
   $ X = span(V_k) $ 라고 가정해보자
   가정에 의해 $u_{k+1} \in X$는 나머지 $u_1, ..., u_k,v_{k+1}, ... ,v_n$의 선형조합으로 표현할 수 있다.  
   $a_1 u_1 + ... + a_k u_k + a_{k+1} u_{k+1}+a_{k+2} v_{k+1} + ... + a_{n+1} v_n = 0$에서 $u_{k+1}$ 때문에 위 식을 만족하려면 0이 아닌 $\alpha$들이 있을 것이다.  

   - 0이 아닌 계수는 어디에 있을 것인가?
     - $a_{k+2} ... a_{n+1}$ 사이에 있다.
       - 만일 위 구간에 0이 아닌 계수가 없다면. 즉 모두 0이라면 0이 아닌 계수는 $\alpha_1, ... , \alpha_{k+1}$ 사이에 있어야 한다.
       - 즉 $\alpha_1 u_1 + ... +\alpha_k u_k + \alpha_{k+1} u_{k+1} = 0$ 이다.
       - $\because U$ 는 선형독립이므로, $\alpha_1 = ... = \alpha_k = 0$ 이다.
       - $\alpha_{k+1} = 0$ 이 된다. $\rightarrow$모든 계수가 0이 되어 가정에 모순된다.
       - $\therefore$ 0이 아닌 계수는 $a_{k+2} ... a_{n+1}$   
   - 0이 아닌 계수를 $\alpha_{k+2}$ 라고 해보자
     - $\alpha_{k+2}v_{k+1} = -\alpha_1 u_1 - ... - \alpha_{n+1} v_n$
     - $\rightarrow v_{k+1} = \text{ linear combination of } \{u_1, ... ,u_{k+1},v_{k+2},...,v_n\}$
     - 즉 $u_{k+1}$을 이용해 $v_{k+1}$을 대체할 수 있다는 뜻
   - $$V_{k+1}= \{ u_1, u_2, ... ,u_k,u_{k+1},v_{k+2}, ...., v_n\}$$이 되며
   - $X = span(V_{k+1})$ 이 된다.  
  
  위 과정을 $k=1,...,n$까지 하게 되면 $V_n={u_1,...u_n}$이 되게 된다. 즉 $X=span(V) \rightarrow X=span(V_n)$  

  처음 시작할 때 가정에서 $m>n$이라고 했으니 $u_{n+1} \in U$이다. 
  $u_{n+1} \in X$이고 $X=span(V_n)$이므로, $u_{n+1} \in U$는 $U$가 선형 독립이 아니라는 뜻이 된다. 이는 모순적이므로 $U$가 선형독립이기 위해서는 $m \leq n$ 이어야 한다.  
  

## Theorem 2

$$ 
(X,F) : \text{vector space} \\
V = \{v_1, v_2, ... ,v_n\} \subset X, V \text{ is a basis for } X \\
U = \{u_1, u_2, ... ,u_n\} \subset X, U \text{ is a basis for } X \\
\rightarrow m=n
$$

## Def. of Dimensions

$$
basis\text{의 개수를 } dimension(=dim(X))\text{이라고 한다.}
$$

# 2. Change of basis  

$$
(X,F) : \text{vector space} \\
V = \{v_1, v_2, ... ,v_n\} \in X, V \text{ is a basis for } X \text{라고 하자}\\
W = \{w_1, w_2, ... ,w_n\} \in X, W \text{ is a basis for } X \text{이면, } \\
x (\in X )\text{를 계수 }\alpha \text{와 }V\text{의 선형조합으로 표현할 수도 있고}, \\
\text{또 다른 계수 }\beta \text{와 } W\text{의 선형조합으로 표현할 수 있다.}
$$

Change of Basis에서는 $\alpha \leftrightarrow \beta$와의 관계를 알아본다.

## 알아봅시다!  
basis $V$의 i번째 column vector를 basis $W$의 선형결합으로 쓸 수 있다.  
$P_{ij}$는 임의의 선형 결합 계수.
$$
x \in X, \\
x = [v_1 ... v_n]\alpha = [w_1 ... w_n]\beta \\
v_i := \text{i 번째 column vector를 }  \\
= [w_1 ... w_n]\begin{bmatrix} P_{1i} \\ P_{2i} \\ ... \\ P_{ni} \end{bmatrix} \\
$$

이를 $i=1 ... n$으로 확장하면 다음과 같다.

$$
\rightarrow [v_1 ... v_n] = [w_1 ... w_n]
\begin{bmatrix} P_{11} & ... & P_{1n} \\ P_{21} & ... & P_{2n} \\ ... &... &... \\ P_{n1} & ... & P_{nn} \end{bmatrix}
$$

$$  
x = [v_1 ... v_n] \alpha \\
= [w_1 ... w_n] \begin{bmatrix} P_{11} & ... & P_{1n} \\ P_{21} & ... & P_{2n} \\ ... &... &... \\ P_{n1} & ... & P_{nn} \end{bmatrix} \alpha \\
= [w_1 ... w_n] \beta 
$$

위와 같은 사실로부터 아래의 결과를 도출할 수 있다.  
$$
\beta= \begin{bmatrix} P_{11} & ... & P_{1n} \\ P_{21} & ... & P_{2n} \\ ... &... &... \\ P_{n1} & ... & P_{nn} \end{bmatrix} \alpha
$$


# 3. Linear transformations, null spaces, and range spaces

## Linear transformations 
줄여서 LT라고 부르기도 한다.  

$$
(X,F), (Y,F) : \text{vector space} \\
$$

$(X,F)$를  $(Y,F)$로 다음과 같이 transformation 하는 함수 L을 linear transformation이라고 부른다.  

1) $L(\alpha x)= \alpha L(x), \forall x \in X, \forall \alpha \in F$  
2) $L(x_1 + x_2) = L(x_1) + L(x_2), \forall x_1, x_2 \in X$  
3) $L(0) = 0$

## Range Space

The range space $R(L)$ of a linear transformation $L$ from $(X,F)$ into $(Y,F)$ is a subset of $(Y,F)$ defined by $$R(L) := \{y \in Y : y=L(x) \text{for some } x \in X \}$$  

즉 입력($x$)에 대해서 선형 변환 후 나올 수 있는 모든 결과($y$)들의 집합

- $R(L)$은 $(Y,F)$의 subspace이다.

## Null space

The null space $N(L)$ of a linear transformation $L$ from $(X,F)$ into $(Y,F)$ is a subset of $(Y,F)$ defined by $$N(L) := \{x \in X : L(x) = 0\}$$  

선형변환하고 봤더니 결과($y$)가 0으로 나오는(맵핑되는) 모든 입력($x$)들의 집합  

- $N(L)$은 $(X,F)$의 subspace이다.  

## Theorem   

$ L : (X,F) \rightarrow (Y,F), \text{ linear transformatoin}$ 일 때 다음의 말은 모두 같은 말이다.  
1) The mapping $L$ is one to one  
2) $N(L)$ is trivial, that is $N(L)={0}$  
3) $L$ maps linearly independent vectors in $X$ into a linearly independent vectos in $Y$  

**proof** $2 \rightarrow 1$
- pick $x,v \in X$
- lets $L(x) = L(V)$
  - $L(x) - L(v) = 0 = L(x-v)$
  - $\because N(L) = {0} \rightarrow x-v=0 \rightarrow x=v$

**proof** $1 \rightarrow 2$  
- lets $N(L) \neq {0}$
  - $L(x) = 0, for x \in N(L), x\neq 0$
- $L(0) = 0 (\because L \text{ is linear transformation})$
- $x$는 0이 아닌데, 0으로 가는 입력값에 0이 있음
- one-to-one(1의 전제)가 깨진다.  
- 2번이 아니면 1번이 아니다(대우)를 보였으니 1번이면 2번인 것  

**proof** $2 \rightarrow 3$
- linearly independenent vectors $v_i \in X, i=1 ... k$
- $ w_i = L(v_i), i=1 ... k $
- lets $\alpha_1 w_1 + ... + \alpha_k w_k = 0$
- $\alpha_1 w_1 + ... + \alpha_k w_k = L(\alpha_1 v_1 + ... +\alpha_k v_k)  $
- $\because N(L)={0} \rightarrow \alpha_1 v_1 + ... +\alpha_k v_k = 0 $
- $\because v_i \text{ is linearly independent} \rightarrow \alpha_1 = ... =\alpha_k = 0$
- $\therefore w_i \text{ is also lineary independent} $  


**proof** $3 \rightarrow 2$  
- lets $N(L) \neq {0}$
- $N(L) \subset X$
- nullspace에 속하는 원소$x(\neq 0)$로 만든 집합 $$\{x\}$$은 [linearly independent](/선형대수학%20치팅시트/2021/08/11/vectorspace.html#4-linear-independence)
- 이 $x$를 $L$로 씌우면 $$\{L(x)\} = \{0\} $$ 인데, $$\{0\}$$은 linearly dependent 임.
- 2번이 아니면 3번도 아님(대우)을 보였으므로 2번이면 3번인 것.  


## Nullity and Rank  
- nullity : $N(L)$의 dimension
- rank : $R(L)$의 dimension

## Dimension Theorem  

$$
dim(X) = nullity(L) + rank(L) = dim(N(L)) + dim(R(L))
$$


# 4. Matrix representations and linear transformations  

선형 변환은 행렬 곱으로 나타날 수 있다!!

$X,Y : \text{vector space}$라고 할 때 $x\in X$는 $X$의 basis vector들의 선형 결합, $y \in Y$는 $Y$의 basis vector들의 선형 결합이고, $L$은 이 선형 결합 계수를 적당히 잘 변환해주는 장치인 셈이다.  

basis가 정해지면 계수로 vector space 내 임의의 vector를 특정할 수 있으므로 $X$와 $Y$의 basis를 정의한 후에는 선형 변환 $L$을 행렬로 표현할 수 있다.  

$$
V := \text{ basis of X} \\
W := \text{ basis of Y} \\
A = [L]_{V,W} := \text{ basis } V \rightarrow \text{basis} W \text{ 로 가는 선형 변환 행렬}  
$$  


## $A$는 어떻게 찾을까?  
$X$의 basis를 $L$을 통해 $Y$로 보내고 해당 vector를 $Y$의 basis $W$의 선형결합으로 표현한다.  

$$
\begin{bmatrix} Lv_1 & ... & Lv_n\end{bmatrix} 
= \begin{bmatrix} w_1 & ... & w_n\end{bmatrix}
  \begin{bmatrix}
  \alpha_{11} & ... & \alpha_{1n} \\
  ... & ... & ... \\
  \alpha_{n1} & ... & \alpha_{nn} \\
  \end{bmatrix} \\

\rightarrow   \begin{bmatrix}
  \alpha_{11} & ... & \alpha_{1n} \\
  ... & ... & ... \\
  \alpha_{n1} & ... & \alpha_{nn} \\
  \end{bmatrix} = A
$$  

임의의 vector $x \in X$를 $R(L)$로 보낸다고 해보자  

$$
x = \gamma_1 v_1 + ... + \gamma_n v_n \\
L(X) = L(\gamma_1 v_1 + ... + \gamma_n v_n) \\
= \gamma_1 L(v_1) + ... + \gamma_n L(v_n) \\
= \begin{bmatrix} Lv_1 & ... & Lv_n \end{bmatrix} \begin{bmatrix} \gamma_1 \\ ... \\ \gamma_n \end{bmatrix} \\
= \begin{bmatrix} w_1 & ... & w_n\end{bmatrix}
  \begin{bmatrix}
  \alpha_{11} & ... & \alpha_{1n} \\
  ... & ... & ... \\
  \alpha_{n1} & ... & \alpha_{nn} \\
  \end{bmatrix} \begin{bmatrix} \gamma_1 \\ ... \\ \gamma_n \end{bmatrix} \\
= \begin{bmatrix} w_1 & ... & w_n\end{bmatrix} A \gamma \\
= \begin{bmatrix} w_1 & ... & w_n\end{bmatrix} \beta  \\

\rightarrow \beta = \begin{bmatrix} \beta_1 \\ ... \\ \beta_n \end{bmatrix} = A\gamma 
$$


### Examples

1. 미분  $d \over ds$


$$
 R_3(s) = span(\{1,s,s^2\}) \\
 R_2(s) = span(\{1,s\}) \\
 
 R_3 \overset{L}{\longrightarrow} R_2
$$

$$  
 \begin{bmatrix} L(1) & L(s) & L(s^2) \end{bmatrix} = \begin{bmatrix} 0 & 1 & 2s \end{bmatrix} \\ 
 = \begin{bmatrix} 1 & s \end{bmatrix} \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \end{bmatrix} \\

 \rightarrow A =  \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \end{bmatrix}
$$

## Similarity Transformation  
두 정방행렬(n by n) $A,B$가 있다. 두 행렬 사이에 $A=T^{-1}BT$로 표현할 수 있는 nonsingular matrix $T$가 있다면, $A,B$는 similar 라고 부른다.  
그리고 이때의 $T$를 similarity transformation 이라고 부른다.  

![diagram](https://lh3.googleusercontent.com/pw/AM-JKLWQG6fcaqZWxVTLkZyGdda4LXbMsXwYizWcTZR-F6kN2rC7T_0o7vXU5EC_EP6qK3mmSexK-DhlyTcdZ8EUZ3VzAuH9jraNqfhJiODABKSwC7KFd0gX5I3dx-9FzfZ7S1AcZvH2eeuhZVv4qWUzSo753w=w1547-h1297-no?authuser=1)

$A$ : $V$ basis에서 $L$을 나타내는 행렬  
$B$ : $W$ basis에서 $L$을 나타내는 행렬  
$P$ : $V \rightarrow W$로 가는 좌표변환 행렬
$P^{-1}$ : $W \rightarrow V$로 가는 좌표변환 행렬  

$A = P^{-1}BP$  
