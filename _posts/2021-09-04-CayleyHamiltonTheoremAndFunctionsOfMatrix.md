---
layout: post
title:  "Cayley-Hamilton Theorem, Functions of a Square Matrix"
description: "Cayley-Hamilton theorem, Polynomial functtions of matrix, Minimal polynomial, Functions of a square matrix"
category: math
---

* TOC
{:toc}  


# Cayley-Hamilton Theorem

- Notation  
    $$A\in C^{n\times n}$$
    $$A^k = A\cdot A\cdot A\cdot ... \cdot A (\text{ k번 행렬 A 곱하기 } )$$
    $$A^0 = I$$

$$\gamma(\lambda) = det(\lambda I - A) = \lambda^n + C_{n-1}\lambda^{n-1} + ... + C_1\lambda+C_0$$ 라고 하자

이때 $$\lambda$$ 자리에 강제로 $$A$$로 치환하여 $$\gamma(A) = A^n + C_{n-1}A^{n-1} +...+C_1A+C_0I$$ 로 바꾸면 $$\gamma(A)=0$$ 이다.

**Proof**

adjoint matrix of $$A$$ 를 다음과 같이 정의한다

$$A=[a_{ij}]
=\begin{bmatrix}a_{11}& a_{12}& ... & a_{1n} \newline
a_{21} &a_{22} & ... & a_{2n} \newline
... & ... & ...& ... & \newline
a_{n1} & a_{n2} & ... &a_{nn}\end{bmatrix} \\
adj(A) = [\alpha_{ij}]^T
=\begin{bmatrix}
\alpha_{11} & \alpha_{21} & ... & \alpha_{n1} \newline
\alpha_{12} & \alpha_{22} & ... & \alpha_{n2} \newline
... & ... & ...& ... \newline
\alpha_{1n} & \alpha_{2n} & ... & \alpha_{nn} \end{bmatrix} \\

\alpha_{ij} = (-1)^{i+j} M_{ij} \\
M_{ij} = \text{ matrix A에서 i행, j열을 지운 matrix의 determinant}$$

$$adj(\lambda I -A)$$ 의 i행 j열 요소들은 matrix $$\lambda I -A$$의 i행 j열을 지운 matrix의 determinant 들이므로 각각의 $$adj(\lambda I- A)$$ 의 요소들은 일종의 $$\lambda$$의 다항식으로 표현된다. 그런데 이때 i행 j열을 지운 것들의 determinant이기 때문에 그 요소들은 최대 $$n-1$$차 다항식으로 표현된다. 각각의 요소에 대해서 $$\lambda$$에 대해 모두 풀어 쓰면 $$adj(\lambda I-A)$$는 계수가 matrix 형태인 $$\lambda$$ 다항식으로 풀어 쓸 수 있다.

$$adj(\lambda I -A) = K_{n-1} \lambda^{n-1} + ... + k_1\lambda + K_0$$

어떠한 행렬 $$A$$ 의 [inverse matrix의 정의가](https://ko.wikipedia.org/wiki/%EA%B0%80%EC%97%AD%ED%96%89%EB%A0%AC) $$ad(A) \over det(A)$$ 이므로,  $${adj(\lambda I - A) \over det(\lambda I-A)}(\lambda I - A) = I$$ 이다.

$$adj(\lambda I -A) (\lambda I -A) = det(\lambda I -A)I$$ 이고, 이를 전개해서 각 계수별로 비교해보면 다음과 같다.

$$\text{우변} : \lambda^n I + C_{n-1}\lambda^{n-1}I + ...+C_1\lambda I + C_0 \lambda  \\
\text{좌변} : K_{n-1} \lambda^n I + ( -K_{n-1} A + K_{n-2} I)\lambda^{n-1} + ... + (-K_0A) \\
$$

$$K_{n-1} = I \\
K_{n-2} I - K_{n-1}A= C_{n-1}I \\
K_{n-3} I - K_{n-2}A = C_{n-2}I \\
...\\
-K_0A = C_0 I$$

위 계수 비교 $$k$$ 번째 줄($$0≤ k ≤n$$) 양변에 $$A^{n-k}$$ 를 곱해서 좌변은 좌변끼리, 우변은 우변끼리 모두 더하면 다음과 같이 식이 전개된다.

$$A^n(K_{n-1} - K_{n-1})+A^{n-1}(K_{n-2}-K_{n-2}) + ... +A^0({K_0 - K_0}) = 0 \\
= A^n + C_{n-1}A^{n-1}+... +C_1A+C_0I \\$$

따라서 $$A^n + C_{n-1}A^{n-1}+... +C_1A+C_0I = \gamma(A)=0$$ 이다.

# Polynomial Function of Matrix( n by n)

polynomial $$f(\lambda) = \sum_{j=0}^{l} a_j \lambda^j$$ 라고 쓸 때 **polynomial function of matrix**는 $$\lambda$$ 자리에 강제로 행렬 $$A$$를 넣은 것을 말한다.

$$f(A) = \sum_{j=0}^l a_j A^j$$

이러한 polynomial function of matrix는 다음과 같은 특성이 있다.

## 1. 만일 $$A$$가 block diagonal matrix라면 ( $$A_i$$ 도 정방행렬)  

$$A = 
\begin{bmatrix}
A_1 & & & \\
    & A_2 & & \\
    &  & ... & \\
    &  & & A_k
\end{bmatrix}
\rightarrow A^m = \begin{bmatrix}
A_1^m & & & \\
    & A_2^m & & \\
    &  & ... & \\
    &  & & A_k^m
\end{bmatrix}$$

$$f(A) = \sum_{j=0}^l a_j A^j = \begin{bmatrix}
f(A_1) & & & \\
    & f(A_2) & & \\
    &  & ... & \\
    &  & & f(A_k)
\end{bmatrix}$$

## 2. $$A$$를 jordan form으로 나타내면 $$A=TJT^-1$$   

$$f(A) = \sum_{j=0}^la_jA^j =\sum a_j(TJT^-1)^j=\sum a_j TJ^jT^{-1}=T(\sum_{j=0}^la_jJ^j)T^{-1} \\
f(A) = Tf(J)T^{-1}$$

## 3. $$f(J)$$ 는 어떤 모습일까?  

Jordan form $$J$$는 Jordan block으로 이루어진 block diagonal matrix이다. 각각의 $$i$$번째 jordan block은 distinct eigenvalue $$\lambda_i$$에 대응되며 $$d$$ 는 distinct eigenvalue의 개수이다. $$i$$번째 jordan block은 $$m_i \times m_i$$로 여기서 $$m_i$$는 algebric multiplicity에 해당한다.

$$J = 
\begin{bmatrix}
J_1 & & & \\
    & J_2 & & \\
    &  & ... & \\
    &  & & J_d
\end{bmatrix}$$

하나의 Jordan block $$J_i$$ 는 다음과 같이 sub-block으로 구성되어 있다. 각각의 sub-block은 eigenvector에 대응되며 $$k$$ 번째 eigenvector에 대한 chain of generalized eigenvector와 연관되어 있다. $$g_i$$는 독립인 eigenvector의 개수, geometric multiplicity 이다. $$k$$ 번째 sub-block의 사이즈는 $$m_{ik} \times m_{ik}$$로 여기서 $$m_{ik}$$는 chain의 개수에 해당한다.

$$J_i = 
\begin{bmatrix}
J_{i1} & & & \\
    & J_{i2} & & \\
    &  & ... & \\
    &  & & J_{ig_i}
\end{bmatrix}$$

chain of generalized eigenvector의 grade는 Index $$\eta$$까지 밖에 못 올라간다.($$N(A-\lambda_i I)^k =N(A-\lambda_i I)^{\eta_i} ,\text{ where } k≥ \eta_i$$ ) 

따라서 $$max(m_{ij})=\eta_i$$ 이다

위 Jordan form의 형태를 생각해보건데 $$f(J)$$는 다음과 같이 쓸 수 있다.

$$f(J) = 
\begin{bmatrix}
f(J_1) & & & \\
    & f(J_2) & & \\
    &  & ... & \\
    &  & & f(J_d)
\end{bmatrix}
\\
= \begin{bmatrix}
f(J_{11}) & & & & &\\
    & f(J_{12}) & & & &\\
    & & ... & & &\\
    & & & ... & & \\
    & & & & ... & \\
    & & & & & f(J_dg_d)\\
\end{bmatrix}$$

## 4. $$f(J_{ij})$$는 어떤 형태일까?

표기를 간단하게 하기 위해 다음과 같이 적도록 하자.

$$J_{ij} \rightarrow J \\
\lambda_i \rightarrow \lambda \\
m_{ij} \rightarrow m \\$$

여기서 $$i$$ 는 $$i$$번째 eigenvalue와 대응되는 index이고 $$j$$는 $$J_i$$ 의 $$j$$번째 sub-block에 대응되는 index이고, $$m_{ij}$$는 $$J_{ij}$$의 행 개수(이자 열 개수) 혹은 이와 대응되는 chain of generalized eigenvector의 개수이다.

이러한 subblock $$J$$는 다음과 같이 표기할 수 있다.

$$J = \lambda I + N \\
N= \begin{bmatrix}
0 & 1 & & & \\
& 0 & 1 & & \\
& & ... & ... & \\  
& & & 0 & 1 \\
& & & & 0 \end{bmatrix} \text{ m by m}$$

$$N$$은 대각성분이 모두 0이고 그 바로 윗줄에 1이 있는 것이다. 이러한 행렬 $$N$$의 특징은 거듭제곱할수록 1이라 적혀 있는 대각성분이 위로 한칸씩 밀리고 밀린 자리에는 0이 채워진다는 것이다.  그래서 $$N^k = 0 \text{ where } k≥m$$ 이다.

따라서 $$J^k$$는 다음과 같이 쓸 수 있다.

$$J^k = (\lambda I + N)^k = {k \choose 0} \lambda ^k N^0 +{k \choose 1} \lambda ^{k-1} N + ... +{k \choose k} \lambda^0 N^k \\
= \sum_{j=0}^k {k \choose j} \lambda ^{k-j}N^j \\
= \sum_{j=0}^{m-1} {k \choose j}\lambda^{k-j}N^j $$

$$k≥m$$ 이면 $$N^k=0$$ 이므로 $$J^k= \sum_{j=0}^{m-1} {k \choose j}\lambda^{k-j}N^j$$ 로 써도 되고 $$k<m$$이라 할 지라도 $${3 \choose 10}=0$$ 이듯이 $${k \choose j}=0 (\text{ where } j≥k)$$ 이기 때문에 $$J^k= \sum_{j=0}^{m-1} {k \choose j}\lambda^{k-j}N^j$$ 이다.

따라서

$$f(J) = \sum_{k=0}^l a_kJ^k = \sum_{k=0}^l a_k\sum_{j=0}^{m-1} {k \choose j} \lambda^{k-j}N^j = \sum_{j=0}^{m-1}N^j \sum_{k=0}^l a_k {k \choose j}\lambda ^{k-j} \\
= \sum_{j=0}^{m-1}N^j \sum_{k=0}^l a_k {k(k-1) ... (k-(j-1)) \over j!} \lambda ^{k-j} \\
= \sum_{j=0}^{m-1}N^j {1\over j!} f^{(j)}(\lambda)$$

$$f^{(j)}(\lambda) = {d^j \over dt^j}f(\lambda)$$

따라서 i번째 Jordan block의 j번째 sub-blcok $$J_{ij} (=\text{ 여기서는 }J)$$ 에 대해서 $$f(J) = \sum_{j=0}^{m-1}N^j {1\over j!} f^{(j)}(\lambda)$$ 이다. 여기서 $$N^j$$ 는 일종의 placeholder matrix 역할을 하는데 이를 풀어써보면

$$f(J) = \sum_{j=0}^{m-1}N^j {1\over j!} f^{(j)}(\lambda) \\
= \begin{bmatrix}
f(\lambda) & f'(\lambda) & {1 \over 2!}f^{(2)}(\lambda) & & ... & {1 \over (m-1)!}f^{(m-1)}(\lambda)  \newline
& f(\lambda) & f'(\lambda) & {1 \over 2!}f^{(2)}(\lambda) & ...& ... \newline
& & f(\lambda) & f'(\lambda) & ...& ... \newline
& & & ... & ...& ... \newline
& &  & & & {1 \over 2!}f^{(2)}(\lambda) \newline
& & & & & f'(\lambda) \newline
    & & & & & f(\lambda)
\end{bmatrix}$$

따라서 $$f(A) = Tf(J)T^{-1}$$ 이고 $$f(J)$$ 는 $$f(\lambda_i), f'(\lambda_i), ... , f^{(\eta_i-1)}(\lambda_i), (i=1,...d)$$ 를 알면 만들 수 있다.

즉 어떠한 polynomial $$f(x)$$에 대해서 $$f(A)$$를 구하기 위한 정보로는 $$A$$의 모든 distinct eigenvalue $$\lambda_1, ... ,\lambda_d$$에 대해서 $$f^{(j)}(\lambda_i), \text{ where } (i=1,...d), (j=0,...,\eta_i-1)$$만 알면 $$f(A)$$를 구할 수 있다.

# Minimal Polynomial

$$\gamma(\lambda) = det(\lambda I -A)$$ 일 대 

임의의 polynomial $$f(\lambda) = \gamma(\lambda )Q(\lambda) + R(\lambda)$$ 로 적을 수 있다. 여기서 $$\gamma(\lambda)$$가 $$n$$차 이므로 $$R(\lambda)$$는 최대 $$n-1$$차이다.

$$\lambda$$를 $$A$$로 치환시켜셔 polynomial of matrix 를 보면 cayley-hamilton theorem 때문에 다음과 같이 쓸 수 있다.

$$f(A) = \gamma(A) Q(A) + R(A) = R(A)$$

**Example** 

이를 이용하면 matrix의 거듭제곱을 쉽게 구할 수 있다. 

가령 $$f(A) = A^{100}, A=\begin{bmatrix} 1 &2 \newline 3&4\end{bmatrix}$$ 를 구해보자. 

$$f(\lambda)=\gamma(\lambda)Q(\lambda)+R(\lambda)$$로 쓸 수 있고, $$\gamma(\lambda)$$는 $$A$$가 2by2 matrix이므로 2차 다항식이다. 따라서 $$R(\lambda)$$는 1차 다항식 $$R(\lambda) = a_0 + a_1\lambda$$로 쓸 수 있다. 

$$A$$의 distinct eigenvalue가 2개 있다면, $$f(\lambda_1) = a_0 + a_1\lambda_1$$, $$f(\lambda_2) = a_0 + a_1\lambda_2$$로 $$a_0, a_1$$을 구할 수 있다.

$$a_0, a_1$$을 구하면 $$f(\lambda) = \gamma(\lambda)Q(\lambda) + (a_0 + a_1\lambda)$$ 이고 $$f(A) = \gamma(A)Q(A) + (a_0 I+ a_1A)=a_0 I + a_1A$$ 로 바로 $$A^{100}$$을 구할 수 있다.

어쨌든 여기서$$\gamma(\lambda)$$ 대신 무엇을 넣으면  나머지 $$R(\lambda)$$의 차수를 줄일 수 있는지 찾고자 하는데, 이 때 $$\gamma(\lambda)$$보다 더 낮은 차수의 다항식을 넣을 수 있다면 $$R(\lambda)$$의 차수도 줄일 수 있을 것이다.이때의 polynomial을 $$\mu(\lambda)$$로 표기하며 정의는 다음과 같다.

$$\mu(\lambda) \leftarrow \mu(A)=0 \text{인 가장 낮은 차수의 다항식}$$

계산의 편의상 $$\mu(\lambda)$$의 최고차항 계수는 1로 하며 다음과 같이 계산한다.

$$\mu(\lambda) = \Pi_{i=1}^d (\lambda -\lambda_i)^{\eta_i}$$

참고로 $$\gamma(\lambda) = det(\lambda I -A) = \Pi_{i=1}^d (\lambda - \lambda_i)^{m_i}$$ 로 계산할 수 있다. 

$$m_i$$는 $$\lambda_i$$의 algebric multiplicity이고 $$\eta_i$$는 $$\lambda_i$$의 index이다. $$m_i$$는 Jordan block의 크기를 결정하고 $$\eta_i$$는 Jordan block의 단일 sub-block 크기의 상한선($$max(m_{ij}) = \eta_i$$) 를 결정한다는 것을 상기해볼 때 $$\eta_i ≤m_i$$ 임을 알 수 있다.

**Proof :** $$\mu(A) = 0$$ 인가?

$$\mu(\cdot)$$는 polynomial 이기 때문에 $$\mu(A) = \mu(TJT^{-1})=T\mu(J)T^{-1}$$ 이다. 따라서 $$\mu(A) = 0$$인가? 라는 질문은 $$\mu(J)=0$$인가? 라는 질문으로 다시 쓸 수 있다.

$$\mu(J) = \Pi_{i=1}^d (J-\lambda_iI)^{\eta_i}$$

인데 $$J$$는 Jordan form 이므로 $$(J-\lambda_1I)$$ 은 첫번째 Jordan block의 대각성분이 0이고 나머지 대각성분은 0이 아니다. $$(J-\lambda_2I)$$는 두번째 Jordan block의 대각성분이 0이고 나머지 대각성분은 0이 아니다. → $$(J-\lambda_j I)$$는 j번째 Jordan block의 대각성분이 0이고 나머지 대각 성분은 0이 아니다.

한편 $$(J-\lambda_1I)^{\eta_1}$$는 첫번째 Jordan block 대각성분의 0 때문에 첫번째 Jordan block 영역이 모두 0이 된다. $$(J-\lambda_2I)^{\eta_2}$$ 는 두번째 Jordan block 대각성분의 0 때문에 두번째 Jordan block 영역이 모두 0이 된다. → $$(J-\lambda_j I)^{\eta_j}$$는 j번째 Jordan block 대각성분의 0 때문에 j번째 Jordan block 영역이 모두 0이 된다. 

한편 block diagonal matrix의 곱은 서로의 block끼리만 곱해진다. 따라서 $$\mu(J)=(J-\lambda_1I)^{\eta_1}(J-\lambda_2I)^{\eta_2} ...(J-\lambda_dI)^{\eta_d}$$ 의 첫번째 Jordan block 영역은 $$(J-\lambda_1I)^{\eta_1}$$ 때문에 모두 0이 되고, 두번째 Jordan block 영역은 $$(J-\lambda_2I)^{\eta_2}$$ 때문에 모두 0이 된다. → j번째 jordan block 영역은 $$(J-\lambda_jI)^{\eta_j}$$ 때문에 모두 0이 된다.

따라서 모든 Jordan block 영역이 0이 되므로 $$\mu(J)=0 \rightarrow \mu(A)=0$$ 이다.

# Functions of a Square Matrix

이제 polynomial 뿐만이 아니라 일반적인 함수 매개변수에 행렬을 넣어보고 싶은 것이다. 가령 $$sin(A), e^{At}$$ 는 어떻게 계산해야 할 지 알고 싶은 것이다. $$sin(A), e^{At}$$  ****이러한 표기들을 어떻게 계산하여야 편리하게 쓸 수 있는지 이 파트에서 정의한다.

## 서로 다른 polynomial $$f(\lambda), g(\lambda)$$ 에 대해서

서로 다른 polynomial $$f(\lambda), g(\lambda)$$ 에 대해서 만일 행렬 $$A$$의 distinct eigenvalue $$\lambda_i, i=1,...,d$$ 에 대해 $$f(\lambda_i)=g(\lambda_i)$$ 이고 $$\eta_i-1$$ 차 미분 계수가 같다고 해보자. 이 경우 $$f(A)=g(A)$$ 이다.

왜냐하면 $$f(A)=Tf(J)T^{-1}, g(A)=Tg(J)T^{-1}$$이고, $$f(J), g(J)$$ 모두 distinct eigenvalue에서의 함수값과 $$\eta_i -1$$차 미분계수만을 사용하여 구성되기 때문이다.

따라서 서로 다른 polynomial이라 할 지라도 주어진 행렬 $$A$$의 모든 distinct eigenvalue에서의 함수값과 모든 distinct eigenvalue의 $$\eta_i -1, (i=1,...,d)$$ 차 까지의 미분계수가 같다면 $$f(A)=g(A)$$가 되는 것이다.

## Polynomial이 아닌 $$f(\cdot)$$에 대해서도

위와 같은 아이디어에 착안하여 다항식이 아닌 함수에 대해서도 같은 개념을 적용해볼 수 있다.

만일 주어진 행렬 $$A$$f(\lambda)$$ 모든 distinct eigenvalue에 대해서 $$f$$의 함수값과 $$f$$의 $$\eta_i -1 , (i=1,..,d)$$ 차 미분 계수가  어떠한 polynomial $$P$$의 함수값과 미분계수와 같다면,

다음과 같이 정의내릴 수 있을 것이다.

$$f(A) = P(A)$$

이러한 polynomial은 항상 존재하고 유일하며 [Hermite interpolation polynomial](https://en.wikipedia.org/wiki/Hermite_interpolation) 이라고 한다.

- $$P(\cdot)\text{의 최대 차수 } < \eta =\sum_{k=1}^d \eta_k$$

## Example

- Exmpale1

    $$A=\begin{bmatrix}-4 & 1 \newline 3 & -2\end{bmatrix}$$, $$e^{At}=?$$

    $$\gamma(\lambda) = det(\lambda I - A) = (\lambda + 4)(\lambda +2) -3 = \lambda^2 +6\lambda +5 = (\lambda+1)(\lambda+5)$$ 

    eigenvalue $$\lambda_1 = -1, \lambda_2 = -5$$ → $$\eta_1 =1, \eta_2 = 1$$ $$(\because d=2, m_1=1, m_2=1)$$

    $$f(\lambda) = e^{\lambda t} \\
    f(\lambda_1) = e^{-t} = P(\lambda_1)\\
    f(\lambda_2) = e^{-5t} = P(\lambda_2)$$

    $$P$$의 최대 차수는 $$\eta = \sum \eta_k=1+1=2$$ 보다 작으므로 $$P(\lambda) = a_0 + a_1 \lambda$$ 이다.

    $$e^{-t} = a_0+a_1(-1)\\
    e^{-5t} = a_0 +a_1(-5) \\
    \rightarrow \\
    a_0 = {5 \over 4}e^{-1t} -{1\over 4} e^{-5t} \\
    a_1 = {1 \over 4}(e^{-t} -e^{-5t})$$

    따라서 

    $$e^{At} = P(A) = ({5 \over 4}e^{-1t} -{1\over 4} e^{-5t})I +  {1 \over 4}(e^{-t} -e^{-5t})A$$

- Example 2

    $$A = \begin{bmatrix}
    0 & 0 & -2 \newline
    0 & 1 & 0 \newline
    1 & 0 & 3 \end{bmatrix}, e^{At} = ?$$

    $$det(\lambda I - A)= (\lambda -1)^2(\lambda-2)$$

    $$\lambda_1 = 1 \rightarrow m_1 = 2, g_1=2, \eta_1 = 1$$ 로 계산하면 구할 수 있다.

    $$\lambda_2 = 2 \rightarrow m_2 = 1, g_2=1, \eta_2= 1$$ 로 계산하면 구할 수 있다.

    $$P$$의 최대차수 < $$\eta= \sum \eta_k = 1+1$$ → $$P(\lambda) = a_0 + a_1\lambda$$

    $$f(\lambda_1 ) = e^t = P(\lambda_1) = a_0 + a_1 \lambda_1 = a_0 + a_1 \\
    f(\lambda_2 ) = e^{2t}= P(\lambda_2) = a_0 + a_2\lambda_2 = a_0 + 2a_1$$

    $$a_1 = e^{2t} - e^t \\
    a_0 = 2e^t - e^{2t} \\
    \therefore P(\lambda) = (2e^{t}-e^{2t}) + (e^{2t}-e^{t})\lambda$$

    따라서

    $$e^{At} =  P(A) = (2e^{t}-e^{2t})I + (e^{2t}-e^{t})A$$