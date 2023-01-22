---
layout: post
title:  "Eigenvectors and Diagonalization"
description: "Generalized Eigenvector and Jordan block"
category: math
---

* TOC
{:toc}

# 1. Generalized Eigenvector and Jordan block

## Generalized Eigenvector

eigenvalue $$\lambda_i$$에 대하여 행렬 $$A$$의 generalized eigenspace는 $$\{x:(A-\lambda_iI)^k x = 0 \text{ for some } k\geq 0\}$$로 정의된다.  

$$dim( \text{generalized eigenspace of } \lambda_i) = m_i$$ 이므로 이 generalized eigenspace에서 $$m_i$$ 개의 독립인 vector를 뽑을 수 있는데, 이를 **generalized eigenvector**라고 한다.

$$k=1$$ 인 eigenspace에서 독립인 vector는 eigenvector이며 이는 $$g_i$$ 개이고 우리는 generalized eigenspace에서 eigenvector를 제외하고도 $$m_i - g_i$$개의 독립인 vector를 더 뽑을 수 있다.  

### Generalized Eigenvector of grade $$k$$

generalized eigenvector를 조금 더 구체적으로 살펴보면 grade $$k$$ 에 대해 나눠볼 수 있다.  

$$v \in \text{generalized eigenspace of } \lambda_i \\
(A-\lambda_i I)^k v = 0 \\
(A-\lambda_i I)^{k-1} v \neq 0$$

위 조건을 만족하는 vector $$v$$ 를 **generalized eigenvector of grade** $$k$$ 라고 부르고 $$v_k$$ 라고 적는다.    
즉 $$v_k$$ 는 $$(A-\lambda_i I)^l, l≥ k$$를 곱하면 0이 되고, $$(A-\lambda_i I)^l, l <k$$ 를 곱하면 0이 되지 않는 eigenvector이다. (= k를 키움으로써 이전에는 eigenspace안에 속하지 않았던 vector가 속하게 된 것)     

### Chain of Generalized Eigenvector

$$v := \text{generalized eigenvector of grade k} \\
v_k = v \\
v_{k-1} = (A-\lambda I)v_k \\
v_{k-2} = (A-\lambda I)^2v_{k} \\
... \\
v_1 = (A-\lambda I)^{k-1} v_k$$

$$\{v_1, ... , v_k\}$$ 를 **chain of generalized eigenvector** 라고 한다. 이때 chain of generalized eigenvector는 linearly indepedent하다.    

**proof**

$$\alpha_1 v_1 + ... + \alpha_kv_k =0$$

위 식의 계수가 모두 0임을 보이면 linearly independent이다.  

1. 양변에 $$(A-\lambda I)^{k-1}$$ 을 곱해보자  

    그러면 grade가 $$k-1$$ 이하인 eigenvector들은 모두 0이 된다. 이 경우 $$\alpha_k (A-\lambda I)^{k-1} v_k=0$$ 형태가 되는데, $$v_k$$ 는 grade k인 generalized eigenvector이므로 $$\alpha_k$$가 0이어야 한다.  

2. 위 방법을 $$(A-\lambda I)^{k-2}$$ 부터 $$(A-\lambda I)$$ 까지 한번씩 곱해봐서 $$\alpha_{k-1}, ... \alpha_1$$ 까지 모두 0인걸 확인할 수 있다.    


## Jordan block

한편 이런 상황을 생각해보자  

$$A \in R^{n \times n}, \text{eigenvalue } \lambda, m(\text{ algebric multiplicity }) = n \\
g (\text{ geometric multiplicity }) = 1$$

generalized eigenspace $$N(A-\lambda I )^\eta$$ 를 잡고 $$v_\eta$$ 인 generalized eigenvector of grade $$\eta$$ 를 하나 잡았다고 해보자. $$v_\eta$$ 로부터 chain of generalized eigenvector를 잡을 수 있다.  

만일 $$\eta = n$$ 이라면   

$$v_n = v_\eta \\
v_{n-1} = (A-\lambda I)v_n \\
v_{n-2} = (A-\lambda I)^2 v_n \\
... \\
v_{1} = (A-\lambda I)^{n-1} v_n$$

으로 chain of generalized eigenvector를 잡을 수 있고, 위 식을 아래와 같이 다시 쓸 수 있다  

$$v_{n-1} = Av_n -\lambda v_n \rightarrow Av_n = \lambda v_n +v_{n-1} \\
A\begin{bmatrix} v_1 & v_2 & ... & v_n \end{bmatrix} = \begin{bmatrix} v_1 & v_2 & ... & v_n\end{bmatrix}
\begin{bmatrix}
\lambda & 1 & 0 & 0 &... & 0 \newline
0 & \lambda & 1 & 0 & ... &0 \newline
&&&&... \newline
0 & 0 & 0& 0&... & \lambda 
\end{bmatrix}$$

$$A = \begin{bmatrix} v_1 & v_2 & ... & v_n \end{bmatrix} \begin{bmatrix} \lambda & 1 & 0 \newline
0 & ... & 1\newline
0 & 0 & \lambda
\end{bmatrix}
 {\begin{bmatrix} v_1 & v_2 & ... & v_n \end{bmatrix} }^{-1}
=TJT^{-1}$$

$$\begin{bmatrix} \lambda & 1 & 0 \newline
0 & ... & 1\newline
0 & 0 & \lambda
\end{bmatrix}$$→ 이런 matrix들을 $$A$$ 의 **Jordan block** 이라고 한다.  

만일 $$g=2$$ 이면 chain set이 2개 생길 것이다.  

$$\{v_1, ... v_k\}, \{w_1, ... w_q\}$$  이렇게 생기고 두 chani set을 column vector 삼아 묶으면   

$$A
\begin{bmatrix}
v_1 & v_2 & ... &v_k & w_1 &w_2 & ... &w_q
\end{bmatrix} \\
= \begin{bmatrix}
v_1 & v_2 & ... &v_k & w_1 &w_2 & ... &w_q
\end{bmatrix} 
\begin{bmatrix}
\begin{matrix}
\lambda & 1 & 0 \newline
0 & ... & 1 \newline
0 & 0 & \lambda 
\end{matrix}
& 0 \newline
0 & 
\begin{matrix}
\lambda & 1 & 0 \newline
0 & ... & 1 \newline
0 & 0 & \lambda \newline
\end{matrix}
\end{bmatrix}$$

그림과 같이 Jordan block이 2개의 sub-block으로 나뉘어지는 것을 볼 수 있다. 좌측 상단 block은 $$k\times k$$ , 우측 하단 block은 $$q \times q$$  사이즈를 가진다.  

즉 $$\lambda_i$$ 에 대해서 $$g_i$$ 만큼의 chain을 잘 찾으면 Jordan block을 구성할 수 있다.   

# 2. Chain of Generalized Eigenvector

Jordan block을 구하려면 chain of generalized eigenvector를 잘 찾으면 된다. 어떻게 Chain of generalized eigenvector를 구할 것인가?  

## bottom up 방식

1. eigenvector 하나를 잡는다. $$v_1 \in N(A-\lambda I)$$  
2. grade 1차수 높은 eigenvector를 잡는다. $$v_1 = (A-\lambda I)v_2$$  인 $$v_2$$를 찾는다.  

이런 bottom up 방식은 좋지 못하다. $$det(A-\lambda I) = 0$$ 이고 이는 곧 singular matrix란 걸 의미하며 $$v_1 \in R(A-\lambda I)$$ 를 확신할 수 없다.   

## Top down 방식

표기를 단순하게 하기 위해 아래와 같이 표기한다.

$$\lambda_i \rightarrow \lambda \\
m_i \rightarrow m \\
g_i \rightarrow g \\
\eta_i \rightarrow \eta \\
N(A-\lambda_i I)^k \rightarrow N^k $$

### 상황

- $$N^0 \subset N^1 \subset N^2 \subset ... \subset N^\eta$$ 이다.
- $$v_k= dim(N^k)$$ 라고 하자
    - $$v_1 = g$$ 이고 $$v_\eta$$ = $$m$$ 이 된다.
- $$\mu_k = dim(N^k)-dim(N^{k-1})$$ 라고 하자.
    - $$N^\eta = N^{\eta+1}$$이므로 $$\mu_{\eta+1} = 0$$  이  될 것임을 알 수 있다.

### $$N^{\eta-1}$$의 vector와는 독립인 vector를 $$N^\eta$$에서 찾자. 
(= generalized eigenvector of grade $$\eta$$ 를 찾자.)

1.  $$N^1$$ 에서 $$\mu_1 = v_1$$ 개 만큼의 선형 독립인 vector $$\{u_{11}, u_{12}, ... u_{1\mu_1}\}$$ 를 나열해보자 (즉 eigenvector의 나열)
2. $$N^2$$ 에서 **위에서 고른 vector와 독립인** vector $$\mu_2$$ 개만큼 더 골라보자.  $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}  \}$$  
3. 위 과정을 $$N^\eta$$ 까지 반복한다.  
$$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... , u_{\eta 1}, ... u_{\eta \mu_\eta}  \}$$ → 총 $$v_\eta = m$$ 개의 독립인 vector들이다.  
4. $$u_{\eta 1}$$ ~ $$u_{\eta \mu_\eta}$$는 generlized eigenvector of grade $$\eta$$ 이다.
5. 위 vector들은 chain 관계가 아니므로 chain 관계들로 잘 맞춰진 vector들로 바꿔치기 할 것이다.

### 바꿔치기→ chain으로 만들자

1. $$V_{\eta 1} = u_{\eta 1}, V_{\eta 2} = u_{\eta 2} , ... , V_{\eta \mu_\eta} = u_{\eta \mu_\eta}$$ 라고 하자
2. 아래 grade $$V$$를 다음과 같이 쓸 수 있다.

    $$V_{(\eta-1) 1} = (A-\lambda I) V_{\eta 1},  \\
    V_{(\eta-1) 2}=(A-\lambda I)V_{\eta 2}, \\
    ... , \\
    V_{(\eta-1) \mu_{\eta}} = (A-\lambda I)V_{\eta \mu_\eta}$$

3. 이제 $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... , u_{\eta 1}, ... u_{\eta \mu_\eta} \}$$ 에서 $$u_{(\eta-1)1}$$ ~ $$u_{(\eta-1)\mu_{\eta-1}}$$을  $$V_{(\eta-1)1}$$ ~ $$V_{(\eta-1)\mu_\eta}$$ 로 교체하고자 하는데 개수가 다르다. $$u$$의 개수는 $$\mu_{\eta-1}$$ 개 $$V$$의 개수는 $$\mu_\eta$$ 개이다. 그런데 $$\mu_{\eta-1} ≥\mu_\eta$$ 이다. 왜일까?


    이를 알려면  $$V_{(\eta-1)1}$$ ~ $$V_{(\eta-1)\mu_\eta}$$ 로 교체한 vector set $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
    V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}} \}$$이 선형 독립임을 보이면 된다.

    왜냐하면 일단 $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
    u_{(\eta-1) 1}, ... , u_{(\eta-1) \mu_{\eta-1}}\}$$ 은 $$N^{\eta-1}$$ 에서 선형 독립인 모든 vector들이다. $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
    V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}} \}$$ 또한 $$N^{\eta-1}$$ 에서 고른 vector들이면서 선형 독립이라면 그 개수가 $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
    u_{(\eta-1) 1}, ... , u_{(\eta-1) \mu_{\eta-1}}\}$$보다 작아야 하기 때문이다.

    따라서 $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
    V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}} \}$$ 들이 선형 독립임을 보이면 $$\mu_\eta \leq \mu_{\eta-1}$$을 보일 수 있다.


    선형독립임을 보이기 위해서면, 아래의 식에서 계수가 모두 0임을 보이면 된다.

    $$\alpha_{11} u_{11} + ... +\alpha_{(\eta-2)\mu_{\eta-2}} u_{(\eta-2)\mu_{\eta-2}}+ \alpha_{(\eta-1)1} V_{(\eta -1)1}+ ... +\alpha_{(\eta-1)\mu_{\eta}}V_{(\eta-1)\mu_\eta}=0$$

    일단 **종속** 이라고 가정해보자

    - $$\alpha_{(\eta-1)1}$$ 부터 그 이후 계수들이 모두 0이라면 $$\alpha_{(\eta-1)1}$$  앞에 0이 아닌 계수가 있어야 하는데, $$u_{ij}$$ 는 모두 선형독립인 vector들만 뽑은 것이므로 0이 아닌 계수가 있을 수 없다. 따라서 0 이 아닌 계수는 $$\alpha_{(\eta-1)1}$$ ~ $$\alpha_{(\eta-1)\mu_\eta}$$에 있다.
    - $$\alpha_{11} u_{11} + ... +\alpha_{(\eta-2)\mu_{\eta-2}} u_{(\eta-2)\mu_{\eta-2}}+ \alpha_{(\eta-1)1} V_{(\eta -1)1}+ ... +\alpha_{(\eta-1)\mu_{\eta}}V_{(\eta-1)\mu_\eta}=0$$ 양변에 $$(A-\lambda I)^{\eta-2}$$ 를 곱해보자. $$\alpha_{11} u_{11} + ... +\alpha_{(\eta-2)\mu_{\eta-2}} u_{(\eta-2)\mu_{\eta-2}}$$ 쪽은 모두 0이 된다. 왜냐하면 $$u$$ vector들의 grade보다 높은 지수의 $$(A-\lambda I)$$ 를 곱했기 때문이다.
    - 따라서 위 식은 $$\sum_{k} \alpha_{(\eta-1)k}(A-\lambda I)^{\eta-2}V_{(\eta-1)k} = 0$$ 이 된다.
    - 그런데 $$(A-\lambda I) ^{\eta-2} V_{(\eta-1)k} \neq 0$$ 이므로 $$\sum_{k} \alpha_{(\eta-1)k}(A-\lambda I)^{\eta-2}V_{(\eta-1)k} = 0$$ 를 만족하려면 모든 계수( $$\alpha_{(\eta-1)k}$$ )가 0이어야 한다.
    - 이는 가정에 모순
    - 따라서 위 식은 선형 독립이다.


    $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
    V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}} \}$$가 선형독립이므로 $$\mu_\eta \leq \mu_{\eta-1}$$ 이다.

    위 과정을 반복하면 임의의 $$k$$에 대하여 $$\mu_k \leq \mu_{k-1}$$ 임을 알 수 있고 $$u_{(\eta-1)1}$$ ~ $$u_{(\eta-1)\mu_{\eta-1}}$$을  $$V_{(\eta-1)1}$$ ~ $$V_{(\eta-1)\mu_\eta}$$ 로 교체하고자 할 때 항상 $$\mu_{k-1} - \mu_{k}$$ 개수 만큼의 vector가 모자르다는 걸 알 수 있다.

4. $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
u_{(\eta-1) 1}, ... , u_{(\eta-1) \mu_{\eta-1}}, u_{\eta 1}, ..., u_{\eta \mu_\eta}  \}$$ 에서 $$u_{(\eta-1) 1}, ... , u_{(\eta-1) \mu_{\eta-1}}$$ 를 $$V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}}$$ 로 바꿔치기에는 개수가 모자라다.

    그래서 $$N^{\eta-1}$$ 에서 임의로 $$N^{\eta-2}$$ vector와 독립이 되도록 $$\mu_{\eta-1} - \mu_{\eta}$$ 개 만큼의 독립인 vector를 추가로 골라서 바꿔치기 하면 된다.

1. **바꿔치기** 하면 

    $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
    V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}}, V_{(\eta-1)(\mu_\eta +1)}, ... , V_{(\eta-1)\mu_{\eta-1}}, u_{\eta 1}, ... , u_{\eta \mu_\eta}\}$$가 된다.

    $$V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}}$$ 는 위 grade에서 한 차례 내려온 것이고, $$V_{(\eta-1) (\mu_\eta+1)}, ... , V_{(\eta-1) \mu_{\eta-1}}$$은 내가 $$N^{\eta-1}$$에서 $$N^{\eta-2}$$의 vector와 독립이 되도록 임의로 고른 것이다.

2. 이제 $$u_{(\eta-2)1}, ... , u_{(\eta-2)\mu_{\eta-2}}$$를 바꿔치기 하기 위해  
$$V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}}, V_{(\eta-1)(\mu_\eta +1)}, ... , V_{(\eta-1)\mu_{\eta-1}}$$ 에 $$(A-\lambda I)$$를 곱해서 $$V_{(\eta-2) 1}, ... , V_{(\eta-2) \mu_{\eta}}, V_{(\eta-2)(\mu_\eta +1)}, ... , V_{(\eta-2)\mu_{\eta-1}}$$을 만든다.
1. $$V_{(\eta-2) 1}, ... , V_{(\eta-2) \mu_{\eta}}, V_{(\eta-2)(\mu_\eta +1)}, ... , V_{(\eta-2)\mu_{\eta-1}}$$ 를 만들면 $$\mu_{\eta-1}$$ 이 $$\mu_{\eta-2}$$ 보다 적을 것이므로 적은 개수 만큼 $$N^{\eta-2}$$ 에서 $$N^{\eta-3}$$의 vector와 독립이 되도록 $$\mu_{\eta-2}-\mu_{\eta-1}$$ 개 만큼의 독립인 vector를 골라 아래와 같이 치환할 수 있다.

    $$\{u_{11}, u_{12}, ... u_{1\mu_1}, u_{21}, ... ,u_{2\mu_2}, ... ,
    V_{(\eta-2) 1}, ... , V_{(\eta-2) \mu_{\eta-2}}, V_{(\eta-1) 1}, ... , V_{(\eta-1) \mu_{\eta}}, V_{(\eta-1)(\mu_\eta +1)}, ... , V_{(\eta-1)\mu_{\eta-1}}, u_{\eta 1}, ... , u_{\eta \mu_\eta}\}$$로 치환할 수 있다.

2. 이런 식으로 계속 치환해가면 최종적으로 chain of generalized eigenvector를 구성할 수 있다.
    - $$g$$ 개 만큼의 sub-block이 하나의 jordan block 안에 생기고 jordan block은 $$m \times m$$ 사이즈가 된다.

## 서로 다른 eigenvalue에 대한 chain of generalized eigenvector들이 서로 독립일까?

위 과정은 하나의 eigenvalue $$\lambda_i$$ 에 대한 top down approach 이다. 만일 distinct eigenvalue가 $$d$$개 있다면 서로 다른 eigenvalue에 대해서 chain of generalized eigenvector들을 구할 수 있는데, 과연 이 vector들은 모두 서로 선형 독립일까? 생각해볼 수 있다.

답은 yes이고 이에 대해 알아보자.

$$\alpha_{ijk}$$ : $$\lambda_i$$ 에 대한 grade $$j$$ 의 $$k$$ 번째 계수  
$$V_{ijk}$$ : $$\lambda_i$$ 에 대한 grade $$j$$ 의 $$k$$ 번째 계수

$$\alpha_{111}V_{111} + \alpha_{112}V_{112} + ... +
\alpha_{1\eta_1m_1}V_{1\eta_1m_1} + ... + \alpha_{d\eta_d m_d }V_{d\eta_d m_d}= 0$$

위 식의 계수들 $$\alpha_{ijk}$$가 모두 0임을 보이면 선형독립임을 알 수 있다.

- $$\lambda_1$$, grade $$\eta_1$$에 대한 계수들 $$\alpha_{1,\eta_1,k}$$ ($$1 \leq k \leq m_1$$) 에 대해 먼저 알아보자
    1. $$(A-\lambda_2 I)^{\eta_2}(A-\lambda_3 I)^{\eta_3} ... (A-\lambda_d I)^{\eta_d}(A-\lambda_1 I)^{\eta_1-1}$$ 을 양변에 곱하면 $$\lambda_1$$ 에 대한 eigenvector들은 제외하고 모두 0이 된다.
    2. $$\sum_k (A-\lambda_2 I)^{\eta_2}(A-\lambda_3 I)^{\eta_3} ... (A-\lambda_d I)^{\eta_d}(A-\lambda_1 I)^{\eta_1} \alpha_{1\eta_1 k}V_{1\eta_1 k} = 0$$ 이 되고 좌변은 $$\sum_k \alpha_{1\eta_1 k}(\lambda_1 -\lambda_2)^{\eta_2}(\lambda_1 -\lambda_3)^{\eta_3}...
    (\lambda_1 -\lambda_d)^{\eta_d}V_{11k}$$가 된다. 왜냐하면  $$V_{11k} = (A-\lambda_1 I)^{\eta_1 -1} V_{1\eta_1 k}$$ 로 grade를 1까지 낮춘 vector이기 때문이다. grade를 1까지 낮춘 vector는 eigenvector로 행렬 $$(A-\lambda I)$$로 표시되는 부분이 $$(\lambda_1 -\lambda)$$로 바뀌어 계산되게 된다.
    3.  $$\sum_k \alpha_{1\eta_1 k}(\lambda_1 -\lambda_2)^{\eta_2}(\lambda_1 -\lambda_3)^{\eta_3}...
    (\lambda_1 -\lambda_d)^{\eta_d}V_{11k} = 0$$ 을 만족하려면 $$\alpha_{1\eta_1 k}$$가 모두 0이어야 한다.
- $$\lambda_1$$, grade $$\eta_1 -1$$ 에 대한 계수들이 0인지 알아보려면 아래와 같이 하면 된다.
    1. $$\alpha_{1\eta_1k}=0$$ 임을 알았으니 아래의 식에 $$(A-\lambda_2 I)^{\eta_2}(A-\lambda_3 I)^{\eta_3} ... (A-\lambda_d I)^{\eta_d}(A-\lambda_1 I)^{\eta_1-2}$$ 를 곱해본다. ($$\eta_1 -1 \rightarrow \eta_1 -2$$로 변경됨)

        $$\alpha_{111}V_{111} + \alpha_{112}V_{112} + ... +
        \alpha_{1(\eta_1-1)m_1}V_{1(\eta_1-1)m_1} + ... + \alpha_{d\eta_d m_d }V_{d\eta_d m_d}= 0$$

    2. grade $$\eta_1$$ 에서 했던 대로 동일하게 반복한다.
- 더 낮은 모든 grade에 대해서는 $$(A-\lambda_1 I)$$의 지수를 낮춰가면서 곱해서 모두 0임을 보이면 된다.
- 다른 eigenvalue에 대해서는 $$(A-\lambda_2 I)^{\eta_2}(A-\lambda_3 I)^{\eta_3} ... (A-\lambda_d I)^{\eta_d}(A-\lambda_1 I)^{\eta_1-1}$$ 식에서 $$\lambda_1$$ 자리에 보이고자 하는 $$\lambda$$ 를 위치시킴으로서 곱하는 식을 구성하고 위 방법대로 반복하면 된다. 이 때 $$(A-\lambda I)$$는 commute matrix($$AB=BA$$인 matrix) 이므로 $$(A-\lambda_2 I)^{\eta_2}(A-\lambda_3 I)^{\eta_3} ... (A-\lambda_d I)^{\eta_d}(A-\lambda_1 I)^{\eta_1-1}$$ 식을 좌우로 교환하여 곱하든 결과는 같다.

# Jordan canonoical form

위 과정을 모든 eigenvalue에 대해서 반복하면 어떠한 행렬 $$A$$가 주어졌을 때 distinct 한 eigenvalue $$d$$개 각각의 $$\lambda_k$$ 에 대해서 $$m_k$$, $$g_k$$ 를 알 수 있고, 이를 기반으로 각각의 eigenvalue에 대하여 chain of generalized eigenvector를 구할 수 있다.

이렇게 chain of generalized eigenvector set을 구하면 Jordan canonical form을 만들 수 있는데, 이는 여러개의 대각 성분으로 Jordan block이 이어져 있는 matrix를 의미한다. 하나의 Jordan block은 하나의 eigenvalue와 대응되며 이 jordan block안에도 $$g$$ 개의 sub-block이 있는데, 이 sub-block은 eigenvector와 대응된다. 

- distinct eigenvalue 개수 만큼의 Jordan block for $$\lambda_i$$ ($$m_i \times m_i$$ size) 가 Jordan canonical form에 있다.
    - $$g_i$$ 개 만큼의 sub-block이 jordan block for $$\lambda_i$$ 에 있다.