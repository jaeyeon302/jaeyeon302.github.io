---
layout: post
title:  "Vector Space"
description: "Fields, Vector space, Subspace, Linear independence"
category: math
---

일반적으로 우리가 vector라는 것을 쓸 때 좌표를 이용해서 자주 표현한다.    

$$
 \vec{x} = (a,b) 
$$  

vector는 연산할 때 참 편리한데, $$ \vec{y} = \vec{x_1}+\vec{x_2}$$ 는 좌표 표기방식을 빌어 vector를 표현했을 때 좌표축별로 값을 더해주면 + 연산결과가 나온다. 
vector를 연산할 때 행렬(Matrix)를 자주 사용하여 계산하기도 한다.

$$ 
y= \begin{bmatrix} y_1 \\ y_2 \end{bmatrix} 
    = \begin{bmatrix} A_{11} A_{12} \\ A_{21} A_{22} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = Ax 
$$

이런 좌표말고도 다항식, 혹은 함수들도 모두 vector라는 것으로 표현할 수 있고, 나아가 종래에는 행렬을 이용하여 함수들, 다항식들 등 다양한 요소를 vector로 취급하여 계산할 수 있게 하다.

이를 위해 vector를 일반화하는 vector space에 대해 다뤄볼 필요가 있다.



* TOC
{:toc}

# 1. Field  
Field, $$F$$ : scalar라는 대상들의 집합과 2개의 연산자($$ +, \cdot $$)에 대해 정의되어 있는 구조체  
이때 ($$ +, \cdot $$) 연산자가 만족하는 성질은 다음과 같다.  
1) [덧셈에 대해 닫혀있다.] $$\alpha, \beta \in F, \rightarrow \alpha+\beta \in F$$   
2) $$\alpha + 0 = \alpha, \forall \alpha \in F, 0 \in F$$ 
3) $$\alpha + \beta = \beta + \alpha $$  
4) $$(\alpha+\beta) +\gamma = \alpha + (\beta+\gamma) $$  
5) [덧셈에 대한 역원]  $$\forall \alpha \in F, \alpha+\beta = 0 인 \beta \in F가 있고, 이때 \beta = -\alpha 라고 표기한다.$$  
6) $$\alpha\cdot\beta = \beta\cdot\alpha$$  
7) $$(\alpha \cdot \beta) \cdot \gamma = \alpha \cdot (\beta \cdot \gamma) $$  
8) [곱셈에 대한 역원] $$ 0을 제외하고 \forall \alpha \in F에 대해서, \alpha \cdot \gamma = 1 인 \gamma \in F 가 있고, 이때 \gamma = \alpha^{-1} 이라고 표기한다.$$  

여튼 scalar로 이루어진 집합에 대해 위와 같은 성질을 만족하는 $$ +, \cdot $$이라는 연산자를 만들면, 해당 연산자와 scalar 집합을 field로 부른다.

**Notation** : 
$$\alpha - \beta = \alpha + (-\beta) $$

### Example
- $$ R + \cdot $$  
$$ C + \cdot $$  
Rational function $$ {x^k + ... +d \over x^k_2 + ... b}$$

# 2. Vector space
$$(X,F) = $$ A vector space over a Field $$F$$
$$X$$ : Vector들의 집합  
$$F$$ : Vector space가 정의되는 Field (scalar들의 모음)  
$$+$$ : Vector 끼리의 덧셈
$$\cdot$$ : Vector에 scalar를 곱하는 곱셈 


이때 $$(+,\cdot)$$ 이라는 연산자가 만족하는 성질은 다음과 같다.  
1) $$x_1, x_2 \in X \rightarrow x_1 + x_2 \in X$$  
2) $$x_1 + x_2 = x_2 + x_1 $$  
3) $$ 0 \in X s.t. x+0=x, \forall x in X$$  
4) $$ y = -x \in X s.t. x+y = 0, \forall x$$  
5) $$\alpha \in F, x\in X \rightarrow \alpha \cdot x \in X$$  
6) $$(\alpha \cdot \beta)\cdot x = \alpha \cdot (\beta \cdot x) \forall x \in X, \alpha, \beta \in F $$  
7) $$\alpha \in F \rightarrow \alpha \cdot (x_1 + x_2) = \alpha \cdot x_1 + \alpha \cdot x_2$$  
8) $$ 1 \in X, s.t. x \cdot 1 = x, \forall x \in X$$

**Notation**  
Vecto space $$(X,F) = X_F$$  
특별한 말이 없으면 본 사이트에서 Field는 $$R$$(Real number field)로 두자 $$F=R$$  


### Example  
1) $$(F^n, F)$$  

$$
\begin{bmatrix}
\alpha_1 \\ 
... \\\
\alpha_n \\
\end{bmatrix} \in F^n
$$

$$+, \cdot$$ : elementwise하게 동작하도록 하면  $$(F^n, F)$$  는 vector space 가 된다.

2) $$(F_n[s],F)$$  

$$\alpha s^{n-1} + ... + m = 0 \in F_n[s] $$
$$+, \cdot$$ : 각 차수별로 덧셈하고, 곱셉은 모든 차수에 대해서 scalar를 곱하게 하면 $$(F_n[s],F)$$는 vector space가 된다.

3) $$(C[t_0, t_1], R)$$

$$C[t_0, t_1]$$ : 정의역 폐구간 $$t_0 - t_1$$까지의 연속 함수들의 집합
$$(+,\cdot)$$ : pointwise하게 덧셈하고, 전체 point에 대해 scalar를 곱하게 하면 vector space가 된다.
- Define $$+$$ : $$(f+g)(t) := f(t) + g(t)$$ : 함수 level에서의 덧셈 연산을 Field level에서의 덧셈연산을 이용해 정의
- Define  $$\cdot$$ : $$(c\cdot f)(t) := cf(t)$$ : 함수 level에서의 곱셈연산을 Field level의 $$\cdot$$을 이용해 정의


# 3. Subspace
vector space $$(X,F)$$가 있다고 해보자.  
$$Y \subset X$$, 이고 $$+, \cdot$$은 $$(X,F)$$의 연산자를 그대로 사용했을 때, 두 연산자에 대해서  
$$ y_1, y_2 \in Y, \alpha \in F \rightarrow y_1 + y_2 \in Y, \alpha \cdot y_1 \in F$$ 이면 $$(X,F)$$의 subspace $$(Y,F)$$라고 한다.

## Sum of subspaces
vector space $$(X,F)$$가 있다고 해보자.  
$$Y, Z \in X$$이고 subspace $$(Y,F), (Z,F)$$라고 하자.  
두 subspace의 합은 다음과 같이 주어진다.  
$$Y+Z = {x: x=y+z, y\in Y, z\in Z}$$
$$(Y+Z,F)$$

## Union of Subspaces  
vector space $$(X,F)$$ 가 있다고 해보자.
$$Y, Z \in X$$이고 subspace $$(Y,F), (Z,F)$$라고 하자. 
$$ Y \cup Z := \{x: x\in Y \text{ or } x \in Z\}  \rightarrow $$ subspace일까?? **subspace 아니다**

- example  
  예를 들어 $$Y축 \cup X축 $$ 공간을 생각해보자. 가로축$$(X)$$에서 vector 하나를 가져오고 세로축($$Y$$)에서 다른 vector를 가져와 더하면 계산 결과 vector는 가로축에도, 세로축에도 안속하게 된다. **덧셈에 닫혀있지 않은 셈**

## Intersection of Subspaces
vector space $$(X,F)$$ 가 있다고 해보자.
$$Y, Z \in X$$이고 subspace $$(Y,F), (Z,F)$$라고 하자. 
$$ Y \cap Z:=\{x : x \in Y and x \in Z\}$$는 subspace이다.

## Direct sum of Subspaces
*국문으로는 직합이라고 한다.*  

vector space $$(X,F)$$ 가 있다고 해보자.
$$Y, Z \in X$$이고 subspace $$(Y,F), (Z,F)$$라고 하자.

$$
Y+Z = X \\
Y \cap Z = \{0\}
$$ 이면 $$X$$는 $$Y,Z$$의 direct sum 이라고 말한다

**Notation** : $$X = Y \bigoplus Z$$

- Direct sum은 왜 중요한가
  $$x \in X = Y \bigoplus Z$$ 이면 아래와 같이 쓸 수 있다.  
  $$x = y+z, where y \in Y, z \in Z $$. 그런데 이 이 구성이 유일하다. 왜냐하면 $$Y \cap Z = \{0\}$$ 이기 때문.

    유일성은 $$ x= y+z = u+w, u\in Y, w \in Z$$라고 두고 서로 빼보면 된다.  

    $$
    \displaylines{
        x-x = 0 = y-u+z-w \\
        y - u = w - z \\
        y,u \in Y \rightarrow y-u \in Y (\because Y \text{is subspace of X})\\
        w,z \in Z \rightarrow w-z \in Z (\because Z \text{is subspace of X})\\
        y-u = w-z = 0 (\because Y \cap Z = {0})\\
        \therefore y=u, w=z
    }
    $$


# 4. Linear independence

### Linear combination  
$$ A \subset X, X = \text{vector set of vector space } (X,F)$$  
$$ \text{element of} A = \{v_1 ... v_k\}$$ 일 때
$$\alpha_1 v_1 + \alpha_2 v_2 + ... +\alpha_k v_k  := $$ linear combination
 
### Span
 $$ A \subset X, X = \text{vector set of vector space } (X,F)$$  
$$ \text{element of} A = \{v_1 ... v_k\}$$ 일 때  
$$A$$ 에 속하는 모든 원소를 가지고 만들 수 있는 모든 linear combination의 집합을 $$span(A)$$라고 표기한다.

### Linear depedence vs Linear independence
- **Linear dependence**  
nonempty set $$A \in X, X \text{is vector set of vector space } (X,F) $$ 은 다음과 같은 특성을 보일 때 linear dependence라고 한다. 
$$A$$의 finite set $$\{x_1, x_2, ... ,x_k\}$$를 꺼내고, scalar $$\{\alpha_1, \alpha_2, ... ,\alpha_k \}$$를 고르는데,   
$$
\alpha_1 x_1 + ... +\alpha_k x_k = 0
$$ 식을 만족하는 계수 $$\alpha$$가 0이 아닌 계수들이면 A는 linear depedence이다.

- **Linear independence**  
dependence가 아니면 independence  
$$
\alpha_1 x_1 + ... + \alpha_k x_k = 0
$$  의 계수들이 모두 0이면 linear independent 하다

- **기타 등등 질문들**    
  1) 공집합$$(\{\} or \emptyset)$$ linearly indepedent일까?    
     1. linearly dependent 집합은 nonempty set에대 해서만 정의된다    
     2. linearly independent 집합은 linearly dependent 집합이 아닌 집합을 의미한다.    
     3. 공집합은 linearly dependenr한 집합이 아니므로 linearly independent 집합이다.    

  2) 0이 아닌 vector 하나로 이루어진 집합 $$\{x\}$$는 linearly depedent일까?  
     1. $$\alpha \cdot x = 0$$ 을 만족하는 계수는 0 밖에 없으므로 linearly independent이다    

  3) 0 vector로 이루어진 집합 \{0\}은 linearly dependent일까?    
     1. $$\alpha \cdot 0 = 0 $$을 만족하는 0이 아닌 계수는 무수히 많으므로 linearly dependent이다.   



- **$$span(A) = span(A-\{v\}) \text{ if } v (\in A) \text{ is a linear combination of } A-\{v\}$$**
  - 일반적으로 "같다(=)"를 증명하려면 value에 대해서는 $$x<=y, x>=y$$ 를 하나씩 증명하면 되고, 집합에 대해서는 $$X \in Y, Y \in X$$를 증명하면 된다.
  - proof)
    1. $$span(A-\{v\}) \in span(A)$$  
    $$ \because A-\{v\} \in A \rightarrow span(A-\{v\}) \in span(A)$$    

    2. $$span(A) \in span(A-\{v\})$$  
    $$
    \displaylines{
     span(A) = span(A-\{v\})+span(\{v\})\\
     span(\{v\}) \in span(A-\{v\}) (\because v \in span(A-\{v\})) \\
     \therefore span(A) \in span(A-\{v\})
     }
    $$


# 5. Basis
 Basis $$B$$ of vector space $${X} := B \text{ is linearly independent and }  span(B) = X $$  
 주어진 vector space에서 선형 독립이고 span 하면 X를 다시 만드는 vector들을 고르면 basis가 된다.  
 Basis는 유일하지 않다.  

