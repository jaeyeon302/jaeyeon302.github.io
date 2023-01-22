---
layout: post
title:  "Eigenvalues and Eigenvectors"
description: "Eigenvalues, Eigenvectors, Independent Eigenvectors and Diagonalization, Eigenspace and generalized eigenspace"
category: math
---
* TOC
{:toc}

# 1. Eigenvalues and Eigenvectors

## Def. of invariant subspace

vectorspace $$(X,F)$$가 있다고 하자.  
Linear transformation $$L:X→F$$ 가 있다고 하자.  
subspace $$Y \subset X$$ 이 있다고 하자.  

이때 $$L(Y) \subset Y$$ 인 subspace $$Y$$를 Linear transformation $$L$$에 대한 $$X$$의 invariant subspace라고 한다.

- **Example을 통해 알아보는 Eigenvalue와 Eigenvector의 일반적인 형태**

    $$span({v_1}) = Y$$ 라고 해보자.  

    만일 Linear transformation $$L$$ 에 대해 $$Y$$가 invariant 하다면, $$L(v_{1}) \in Y$$ 이므로, $$L(v_{1}) = \alpha v_1$$으로 쓸수 있고, 상수배가 된다는 걸 알 수 있다.  

    여기서 $$L$$- invariant subspace가 eigenvalue와 eigenvector의 어떤 일반화된 form임을 짐작해볼 수 있다.  

## Def. of eigenvalue(e.v.) and eigenvector(e.vec.)

$$\text{vector space} (X,F), A:\text{Linear transformation } X \rightarrow X$$

만일 $$Ax=\lambda x, x \in X^n -{0}, \lambda \in F(\text{scalar})$$ 인 $$x, \lambda$$ 가 존재한다면 이때의 $$x$$를 eigenvector, $$\lambda$$ 를 eigenvalue라고 한다.

→ 임의의 basis가 주어지면, 어떠한 vector도 basis의 선형결합으로 쓸 수 있고, 이를 column vector 형태로 표현할 수 있으며, 이렇게 표기하면 linear transformation도 matrix 형태로 쓸 수 있다.  
→ 본 페이지에서 다루는 field $$F$$는 complex number $$C$$로 쓸 것이며, vector $$x \in C^n$$이 된다.

## 어떻게 eigenvector, eigenvalue를 구할까?

$$Ax = \lambda x \rightarrow (A-\lambda I)x = 0 $$


$$Ax = \lambda x \rightarrow (A-\lambda I)x = 0 \\ \because x\neq 0 \\ \rightarrow (A-\lambda I) \text{should be singular(=noninvertible) matrix }\\ \rightarrow det(A-\lambda I) = 0$$

$$det(A-\lambda I)=0$$을 만족하는 $$\lambda$$가 eigenvalue가 된다.  이로 인해 다음과 같이 $$\lambda$$의 n차 다항식이 세워진다.

$$det(A-\lambda I) = \lambda^n + ... + k  \\
det(A-\lambda I) = 0 \rightarrow \text{ 특성 방정식}$$

이렇게 n차 $$\lambda$$ 다항식을 풀어서 eigenvalue를 구하고 각각의 eigenvalue에 대해서 $$x\in N(A-\lambda I)$$인 $$x$$를 뽑으면 eigenvalue - eigenvector pair를 구할 수 있다.

## 중첩

n차 $$\lambda$$ 방정식을 풀었는데, $$\lambda$$가 모두 서로 다른 값이 아니라 일부 같은 값이 나올 수 있다. (가령 $$(\lambda - k)^2=0$$ 처럼). 이를 중첩되었다고 말한다. 이때 중첩되지 않고 서로 다르게 나온 eigenvalue들을 **distinct eigenvalue** 라고 말한다.  

distinct eigenvalue가 $$d$$ 개 있다고 하자. 이때 $$d ≤ n(= \text{n by n matrix의 n})$$  

### algebric  multiplicity

$$det(A-\lambda I)=(\lambda -\lambda_1)^{m_1}(\lambda - \lambda_2)^{m_2} .... (\lambda - \lambda_d)^{m_d}= \Pi_{i=1}^d (\lambda -\lambda_i)^{m_i}$$

위 식에서 $$m_i$$를 **algebric multiplicity of** $$\lambda_i$$ 라고 한다.  
즉 $$\lambda_i$$가 몇 번 겹쳤는가.

### geometric multiplicity

$$nullity(A-\lambda_i I)=dim(N(A-\lambda_i I))=g_i$$

$$g_i$$를 **geometric multiplicity**라고 하며 $$\lambda_i$$ 에 대해서 독립인 eigenvector가 몇 개인지를 의미한다.

## Basis가 바뀌면 Eigenvalue와 Eigenvector는?

- **Eigenvalue**는 basis가 바뀌어도 바뀌지 않는다. 왜냐하면 eigenvalue는 general vector $$v$$ on basis  $$V$$ 에 대해서 $$Lv=\lambda v$$ 형태로 정의했기 대문이다.
- **Eigenvector**는 basis가 바뀌면 계속 바뀐다.

# 2. Independent Eigenvectors and Diagonalization

## Theorem 1

$$\lambda_1, \lambda_2, ... , \lambda_d$$  를 matrix $$A$$의 distinct eigenvalues, $$v_i$$ 를 $$\lambda_i$$ 에 대응되는 eigenvector라고 하자.  
그러면 $$set\{v_1, v_2, ... , v_d\}$$ linearly independent이다.

**Proof**

$$\alpha_1 v_1 +... +\alpha_d v_d = 0,\text{ 인 } \alpha_i \text{가 모두 0 인지 아닌지 확인하면 된다.}$$

1) 결론을 부정하여 $$\alpha_i \neq 0$$ 이라고 해보자.  

2) 양변에 $$(A-\lambda_2 I)^{m_2} (A-\lambda_3 I)^{m_3} ... (A-\lambda_d I)^{m_d}$$ 를 곱해본다.  

3) 

$$(A-\lambda_2 I)^{m_2} (A-\lambda_3 I)^{m_3} ... (A-\lambda_d I)^{m_d} \cdot \alpha_i v_i \\ 
= (\lambda_i - \lambda_2 )^{m_2} (\lambda_i - \lambda_3 )^{m_3} ... (\lambda_i - \lambda_d )^{m_d} \cdot \alpha_i v_i$$

중간에 $$(\lambda_i -\lambda_i)^{m_i}$$ 가 있을 것이기 때문에 우변은 무조건 0이 되고 따라서 $$\alpha_i$$ 는 0이 될 수 밖에 없다.

## Theorem 2

$$\lambda_1, ... , \lambda_d$$ 를 matrix $$A$$의 distinct eigenvalues, $$set\{v_{i,1}, ... ,v_{i, g_i}\}$$를 $$\lambda_i$$ 에 대응되는 eigenvector이자 Linearly independent 한 eigenvector라고 하자.  

그러면 $$set\{v_{1,1}, ... , v_{1,g_1}, v_{2,1}, ... ,v_{2, g_2}, ......,  v_{d,1}, ... ,v_{d,g_d}\}$$는 linearly indepdent이다.

 **Proof**

$$\sum_{i=1}^{d} (\sum_{j=1}^{g_i} \alpha_{i,j}\cdot v_{i,j}) = \sum_{i=1} ^d w_i = 0$$

서로 독립인 것들을 모두 더했더니 0이라는 뜻은 모든 $$\forall i, w_i =0$$ 임을 알 수 있다. → $$\alpha_{i,j}=0$$ 이다.

## Diagonalizable

n by n 정방행렬 $$A$$가 n개의 linearly indepdent eigenvector를 가지고 있다면 $$A$$는 **diagonalizable** 하다. → matrix $$A$$에 중복된 eigenvalue가 있다면, 해당 eigenvalue $$\lambda_i$$ 에 대해 gemoetric multiplicity $$g_i$$ 가 algebric multiplicity $$m_i$$랑 같다는 뜻.

$$T^{-1}AT = \Lambda (=\text{대각 성분만 있는 행렬})$$

즉 $$A \text{ is diagonalizable} \leftrightarrow n\text{개의 indep. eigenvector 가 존재한다}$$

**Proof**

$$v_i = \text{ column vector } \\  
A\begin{bmatrix}v_1 & v_2  & ... & v_n\end{bmatrix} = \begin{bmatrix} Av_1 & Av_2 & ... & Av_n \end{bmatrix} = \\ \begin{bmatrix} \lambda_1 v_1 &\lambda_2 v_2 & \lambda_3 v_3 & ... & \lambda_n v_n\end{bmatrix} \\
= \begin{bmatrix} v_1 & v_2 & ... & v_n \end{bmatrix}$$

$$AT = T\Lambda \rightarrow T^{-1}AT=\Lambda$$

 

$$T$$의 $$i$$ 번째 column을 $$v_i$$ 라고 정해주면 그 column이 eigenvalue $$\lambda_i$$의 eigenvector 가 된다.  

- $$A$$가 symmetric 하다면 대각화가 가능하다는 것이 알려져 있다.

    $$\text{symmetric } \leftrightarrow A^H = A \text{ on complex domain}$$  

    - $$A^H$$=Hermitian = matrix $$A$$ 를 transpose하고 element들을 모두 complex conjugate 하는 것

- 만일 eigenvaluer가 모두 distinct eigenvalue이면 $$A$$는 대각화가 가능하다.
- eigenvalue가 중첩이 일어났어도, $$m_i = g_i$$ 면 $$A$$는 대각화가 가능하다.
- 중첩이 일어나고 $$g_i < m_i$$가 되면 대각화가 불가능해지고 이때는 **Jordan form**으로 가야한다.

# 3. Eigenspace and Generalized Eigenspace

## Eigenspace

eigenvalue $$\lambda_i$$ 에 관하여 행렬 $$A$$의 **eigenspace** $$:=$$ set of eigenvectors of $$\lambda_i$$   

$$Eigenspace = \{x : (A-\lambda_i)x = 0\}$$

Eigenspace는 행렬 $$A$$에 대해 invariant 하다. 즉 Eigenspace의 요소 하나를 골라 $$A$$ matrix를 곱해도 여전히 Eigenspace에 속한다는 뜻이다.


$$(A-\lambda_iI)Ax = A(A-\lambda_i I)x = 0 (\because (A-\lambda_i I)x = 0) \\ 
\rightarrow Ax \in \{x : (A-\lambda_i I)x = 0\} (=\text{ eigenspace of } A \text{ associated with } \lambda_i)$$

## Generalized Eigenspace of $$A$$ for $$\lambda$$

eigenvalue $$\lambda$$에 관하여 행렬 $$A$$의 **generalized eigenspace 는**

$$\text{Generalized Eigenspace } = \{x : (A-\lambda I)^k x = 0 \text{ for some } k \geq 0 \}$$

위 경우에서 $$k=1$$ 이면 eigenspace가 되는 것이다.  

### Index $$\eta$$

$$N(A-\lambda I)^0 = \{0\} \\ 
\subset  N(A-\lambda I) = \text{ eigenspace } \\ 
\subset N(A-\lambda I)^2 = ... \subset C^n$$

$$(A-\lambda I)^k x = 0$$ 이 되어버리면 $$(A-\lambda I)^{k+1}= (A-\lambda I)(A-\lambda I)^k x=0$$ 이 되어버리므로 $$k$$인 nullspace는 $$k+1$$인 nullspace안에 포함된다. 즉 $$(A-\lambda I)^k$$ 을 곱해면 0이 되는 $$x$$는 $$(A-\lambda I)^{k+1}$$을 곱해도 무조건 0이되고, $$(A-\lambda I)^k$$ 을 곱해도 0이 안되는 $$x$$가 $$(A-\lambda I)^{k+1}$$ 를 곱하면 0이 될 수도 있으니  $$N(A-\lambda I)^k \subset N(A-\lambda I)^{k+1}$$이 된다.  

그런데 이 $$k$$의 일종의 실질적 상한선이 존재한다.

$$\eta \ s.t. \ N(A-\lambda I)^k = N(A-\lambda I)^\eta , \ k \geq \eta , \eta \leq n$$

즉 $$k$$를 아무리 높여도 특정 값 이상으로는 nullspace를 더 넓힐 수가 없는 것이다. 이때의 $$k$$를 $$\eta$$ 라고 표기하고 **index** 라고 표기한다.

Generalized Eigenspace는 $$\eta$$를 이용하면 다음과 같이도 쓸 수 있다.

$$\text{Generalized Eigenspace } = \{x : (A-\lambda I)^k x = 0 \text{ for some } k \geq 0 \} = N(A-\lambda I)^\eta$$

## Theorem

eigenvalue $$\lambda_i$$ 에 관하여 행렬 $$A$$의 generalized eigenspace의 dimension은 algebrid multiplicity $$m_i$$ 와 같다.

$$dim(\text{ Generalized eigenspace of } A \text{ corresponsding to the eigenvalue } \lambda_i )\\
 = dim(N(A-\lambda_i I)^\eta) = m_i$$


1. 알아두면 좋은 사실  

    $$\begin{bmatrix} 
    0 & * & * \newline 
    0 & 0 & * \newline
    0 & 0 & 0 \newline
    \end{bmatrix}
    \begin{bmatrix} 
    0 & * & * \newline 
    0 & 0 & * \newline
    0 & 0 & 0 \newline
    \end{bmatrix}
    = 
    \begin{bmatrix} 
    0 & 0 & * \newline 
    0 & 0 & 0 \newline
    0 & 0 & 0 \newline
    \end{bmatrix}$$→ 0이 우측 상단으로 하나씩 밀린다.

2. 알아두면 좋은 사실 → Schur's decomposition lemma (triangularization)

    for **any** $$A \in C^{n \times n}$$  
    unitary matrix $$U$$가 존재한다. (여기서 unitary란, $$U^HU=I$$)  
    s.t. $$U^{-1}AU = T \text{ (upper triangular matrix) } = \begin{bmatrix} 
    \lambda_1 & * & * \newline 
    0 & \lambda_2 & * \newline
    0 & 0 & \lambda_3 \newline
    \end{bmatrix}$$

    대각 성분은 $$A$$의 eigenvalue들이다.

3. 알아두면 좋은 사실  

    unitary matrix $$U$$를 적당히 조절하면 중첩된 eigenvalue $$\lambda_i$$ 를 위로 올릴 수 있다.  

    $$U^{-1} A U = T =
    \begin{bmatrix} 
    \lambda_1 & * & * \newline 
    0 & ... & * \newline
    0 & 0 & ... \newline
    \end{bmatrix} =
    \begin{bmatrix}
    T_0 \in C^{m_i \times m_i} & T_2 \newline
    0 & T_1 \newline
    \end{bmatrix}$$  

    $$T_0 =
    \begin{bmatrix} 
    \lambda_i & * & * \newline 
    0 & \lambda_i & * \newline
    0 & 0 & \lambda_i \newline
    \end{bmatrix}$$ 로 만든다는 뜻 그래야 나중에 $$\lambda_i I$$를 뺄때 대각성분 일부를 0으로 날릴 수 있다.

**Proof**

$$N(A-\lambda_i I)^{\eta_i} = N(UTU^{-1} - \lambda_i I)^{\eta_i}$$

$$dim(\text{ Generalized eigenspace of } A \text{ corresponsding to the eigenvalue } \lambda_i )\\
 = dim(N(A-\lambda_i I)^\eta) \\
= dim(N(UTU^{-1}-\lambda_iI)^{\eta_i}) \\
= dim(N(UTU^{-1} - U\lambda_i U^{-1})^{\eta_i}) \\
=dim(N(T-\lambda_i I)^{\eta_i})$$

$${\begin{bmatrix}
A&B\newline
0&C
\end{bmatrix}}^2 = 
\begin{bmatrix}
A^2 & * \newline
0 & C^2
\end{bmatrix}$$임을 생각하면 

$$(T-\lambda_i I)^{\eta_i} = 
{\begin{bmatrix}
0 & T_2 \newline
0 & T_1 - \lambda_i I
\end{bmatrix}}^{\eta_i} =
\begin{bmatrix}
0 & T_2 \newline
0 & (T_1 - \lambda_i I)^{\eta_i}
\end{bmatrix} = 
\begin{bmatrix}
0 & * \newline
0 & @\newline
\end{bmatrix} \\
dim(N(T-\lambda_i I)^{\eta_i}) \\
= n - dim(R(T-\lambda_i I)^{\eta_i})\\
= n - dim(@) = m_i$$


eigenvalue $$\lambda_i$$ 에 관하여 행렬 $$A$$의 generalized eigenspace의 dimension $$m_i$$ 이다. 이제 이 generalized eigenspace에서 임의의 $$m_i - g_i$$ 개수의 독립인 vector를 뽑아내고 이를 뽑아내면 generalized eigenvector라고 부른다. 이를 잘 이용하여 Jordan form을 구성해볼 수 있다.