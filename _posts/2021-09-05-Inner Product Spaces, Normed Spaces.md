---
layout: post
title:  "Inner Product Spaces, Normed Spaces"
description: "Inner product space, Normed space, Gram-schmidt ornomalization, Norm of linear transformation"
category: math
---

* TOC
{:toc}  

# Inner Product Space

Vector space $$X$$ + inner product $$<\cdot, \cdot>$$  = Inner Product Space

## Inner product $$<\cdot , \cdot >$$

아래의 성질을 만족하는 연산을 inner product 라고 한다.

$$x,y \in (X,F)$$ 인 vector에 대해 $$<x,y>\in F$$ 를 출력하는 연산

1. $<x,y>=\overline{<y,x>}$
2. $$<x,ay+bz> = a<x,y>+b<x,z>$$ → 뒤 쪽 argument에 대한 선형성
    $$<ay+bz,x> = \overline{<x,ay+bz>} \\
    = \overline{a<x,y>+b<x,z>}\\
    =\overline{a}<y,x>+\overline{b}<z,x>$$
3. $$<x,x> \geq 0$$ 이고 $$<x,x> = 0$$인 $$x=0$$ 밖에 없다.

### example)

- $$x,y \in (C^n, C)$$ → $$<x,y> = \overline{x}^Ty=x^*y$$
- $$x,y \in (R^n,R)$$ → $$<x,y> = x^Ty$$
- $$x,y \in (C[t_0,t_1], R)$$ → $$<x,y> = \int_{t_0}^{t_1} x(t)g(t)dt$$
    - $$C[t_0,t_1]$$ 는 $$[t_0,t_1]$$에서 정의된 연속 함수
- $$x,y \in (C^n[t_0,t_1], R)$$ → $$<x,y> = \int_{t_0}^{t_1} x(t)^Ty(t) dt$$
    - $$(C^n[t_0,t_1], R)$$ 에 속하는 vector는 가령 이런 것들이 있다. $$\begin{bmatrix} f_1(\cdot), f_2(\cdot), ... , f_n(\cdot)\end{bmatrix}^T$$

## Orthogonal

inner product 연산을 정의함으로서 두 vector가 수직인지 아닌지 이야기할 수 있게 된다.

$$x \perp y \leftrightarrow <x,y> = 0$$

집합 $$A,B$$가 수직이다,라는 뜻은  $$A$$에 속하는 임의의 vector $$x$$와 $$B$$에 속하는 임의의 vector $$y$$ 가 서로 수직이면 집합 $$A \perp B$$ 라고 한다.

$$x \perp y, \forall x \in A, \forall y \in B \leftrightarrow A \perp B$$

## Orthogonal Complement

$$X$$ : inner product space,    
$$Y$$ : subspace of $$X$$  
라고 할 때, 

$$Y$$의 orthogonal complement $$Y^{\perp}=\{x : <x,y>=0, \forall y \in Y\}$$ $$Y$$의 perp라고 말하기도 한다.  
$$Y \cap Y^T = \{0\}$$ 인데, 왜냐하면 $$x\in Y \text{ and } x \in Y^\perp$$ 이면 $$<x,x> = 0$$ 이고 $$<x,x> = 0$$ 을 만족하는 vector $$x$$는 0밖에 없기 때문.

# Normed Space

Vector space $$X$$ + Norm $$\|\cdot\|$$ = Normed space

## Norm $$\| \cdot \|$$

아래의 성질을 만족하는 연산을 Norm이라고 한다.

$$x \in X$$인 vector에 대해 $$\|x\| \in R$$ 를 출력하는 연산
1.  $$\|x\|\geq 0, \forall x \in X$$
만일 $$\|x\|=0$$ 이면 이를 만족하는 $$x=0$$ 밖에 없다
1. $$\|ax\| = a\|x\|$$, $$\forall x \in X, \forall \alpha \in F$$ 
2. $$\|x+y\| ≤ \|x\| + \|y\|, \forall x,y \in X$$  
    [Triangular inequality](https://www.britannica.com/science/triangle-inequality) 라고도 한다.

### example)

$$x \in (R^n, R), x=[x_1 ... x_n]^T$$  
    - 1-norm : $$\|x\|_1 = \sum_{i=1}^{n} |x_i|$$  
    - 2-norm(aka, euclidean norm, frobenius norm) :  $$\|x\|_2 = \sqrt{\sum_{i=1}^n |x_i|^2}$$  
    - infinite norm : $$\|x\|_\infty = max(|x_i|)$$

$$R^n$$ 공간에서 위와 같은 Norm들은 위 Norm의 정의를 모두 만족하는 Norm들이다. 

이를 일반화 하면  
**p-norm :** $$\|x\|_p =( \sum_{i=1}^n |x_i|^p)^{1\over p}$$ $$(1 ≤ p < \infty)$$

## Continuity

Norm이 있으면 함수의 연속성을 이야기할 수 있다.

$$X,Y : \text{Normed space} \\
X \overset{f}{\rightarrow} Y \\$$

인 함수 $$f$$ 에 대해서 $$f$$ 가 $$x=x_0$$ 에서 연속이라면 다음과 같다.

$$\forall \epsilon >0, \exists \delta >0 \\
s.t. \|x-x_0\| \leq \delta \rightarrow \|f(x) - f(x_0)\| \leq \epsilon$$

이는 $$f(x_0)$$를 기준으로 아무리 작은 $$y$$ 값 범위 $$\epsilon$$ 이내의 그 어떤 값을 잡아도 해당 값을 함수로 출력하는 입력값 $$x$$ 가 $$x_0$$를 기준으로 임의의 $$\delta$$ 이내에 존재한다는 뜻.

vector space $$X,Y$$에 norm 이라는 연산자를 도입함으로써 함수 $$f: X \overset{f}{\rightarrow} Y$$ 의 연속성을 이야기할 수 있게 되었다.

# Relationship between inner product space and normed space

$$X$$ 가 Inner Product Space 이면 $$<\cdot, \cdot>$$ 이라는 Inner Product 연산자가 정의되어 있는데, $$<\cdot, \cdot>$$ 이라는 연산자의 성질로 $$\|x\|:=\sqrt{<x,x>}$$ 를 정의하여 Norm으로 쓸 수 있다.

실제로 Norm인지 확인하기 위해 Norm 성질 3가지를 체크해보면 된다.

1. $$\|x\| > 0, \forall x \in X$$ 이고 $$\|x\| = 0 \leftrightarrow x=0$$  
    $$<x,x> > 0, \forall x \in X$$  이고 $$<x,x> =0 \leftrightarrow x=0$$ 이므로 만족
2. $ \|\|\alpha x \|\| = \|\alpha\| \|\|x\|\| $  
    $$\|\alpha x\|=\sqrt{<\alpha x,  \alpha x>} = \sqrt{\alpha,\overline{\alpha}<x,x>}=|\alpha|\sqrt{<x,x>}=|\alpha| \|x\|$$

3. $ ||x+y|| \leq ||x|| + ||y|| $  
    $$\|x+y\|^2 =<x+y,x+y>=<x,x>+<y,x>+<x,y>+<y,y>\\
    = \|x\|^2 + 2Re{<x,y>} + \|y\|^2 \\
    \leq \|x\|^2 + 2|<x,y>| + \|y\|^2 \\
    \leq \|x\|^2 + 2\|x\|\|y\| +\|y\|^2 (\because \text{schwarz inequality})\\
    \\$$

    $$\therefore \|x+y\|^2 \leq (\|x\| + \|y\|)^2$$

    - **Schwarz Inequality**

        $$\|x\|:=\sqrt{<x,x>}\rightarrow <x,y> \leq \|x\|\|y\| \\$$

        왜냐하면

        $$<x+ay,x+ay> = <x+ay,x> + a<x+ay,y> \\
        = <x,x>+\overline{a}<y,x>+a\overline{a}<y,y>+a<x,y> \\
        = \|x\|^2 + \overline{a}<y,x>+ a<x,y>+a\overline{a}<y,y> $$

        $$<x+ay,x+ay> \geq 0, \forall a, \forall x, \forall y \neq 0$$

        $$a = - {\overline{<x,y>} \over \|y\|^2}$$ 이라고 정해보자 그러면

        $$\|x\|^2 + \overline{a}<y,x>+ a<x,y>+a\overline{a}<y,y> \\
        = \|x\|^2 - {|<x,y>|^2 \over \|y\|^2}$$

        $$\|x\|^2 - {|<x,y>|^2 \over \|y\|^2} \geq 0 \rightarrow \|x\|\cdot \|y\| \geq |<x,y>|$$

따라서 Inner Product Space면 Inner product를 이용해 norm을 정의할 수 있고 이로서 Normed space가 된다는 것을 확인했다.

- 참고) $$<x,y> = 0 \rightarrow \|x+y\|^2 = \|x\|^2 + \|y\|^2$$  (피타고라스의 정리)

# Orthonormalization

- Inner product space $$X$$ 에서 basis를 서로 수직인 basis로 잡으면 **Orthogonal Basis** 라고 한다. 여기에 수직인 basis의 Norm이 모두 1이면 **Orthonormal Basis** 라고 한다.
- 집함 $$A$$ 가 Orthonormal 하다라는 것은 $$A$$의 element vector들이 모두 normal vector이고 서로 ㅐorthogonal 하다는 것을 의미한다.
- Example

    $$( C[0,2\pi], R)$$에서

    $$A = \{1,sin(t), cos(t), sin(2t), cos(2t), ... , sin(kt), cos(kt), ... \}$$ 는 orthogonal set이다.

    $$<sin(kt),cos(kt)> = \int_0^{2\pi} sin(kt)cos(kt) dt = \int_0^{2\pi} 0.5sin(2kt)dt = 0$$

    $$\|sin(kt)\| = \sqrt{\pi}$$, $$\|1\| = \sqrt{2\pi}$$

    Orthonormal set으로 만들려면 각각의 element에 $$\|\cdot\|$$을 구해 나눠주면 된다.

## Gram-schmidt Orthonormalization

임의의 독립인 vector로부터 크기가 1이고 서로 수직인 독립인 vector를 유도해내는 과정

$$X : \text{ Inner product space}, \text{독립인 vector} : \{w_1 ,... ,w_n\}, n \leq dim(X)\\
\longrightarrow \exists \{v_1, ... v_n\} \text{orthonormal set, } v_k :=\text{linear combination of }\{w_1, ... w_k\}$$

상식적인 수준인 $$R^3$$ 에서 이를 살펴보자

- Step 1: $$v_1 = { w_1 \over \|w_1\|}$$
- Step 2:  
$$u_2 = w_2 - <v_1,w_2>v_1$$    
$$v_2 = {u_2 \over \|u_2\|}$$   
- Step 3:   
$$u_3 = w_3 - <v_1, w_3>v_1 - <v_2,w_3>v_2$$  
$$v_3 = { u_3 \over \|u_3\|}$$  

위 명제가 $$l$$ 까지 성립한다고 가정하고 $$l+1$$도 성립함을 유도해보자

그리고 $$u_{l+1} = w_{l+1} - \sum_{j=1}^l < v_j,w_{l+1}>v_j$$ 라고 정의해보자

- $$<v_i, u_{l+1}> = 0, (i=1, ... , l)$$

    $$<v_i,u_{l+1}> = <v_i,w_{l+1}>-<v_i,\sum_{j=1}^l < v_j,w_{l+1}>v_j> \\
    = <v_i,w_{l+1}> - <v_i, <v_i,w_{l+1}>v_i> (\because <v_i,v_j>=0 \text{ for } i\neq j )\\
    =<v_i,w_{l+1}>-<v_i,w_{l+1}><v_i,v_i> \\
    = <v_i,w_{l+1}>\cdot(1-\|v_i\|^2)\\
    = 0 (\because \|v_i\|^2 =1)$$

- $$u_{l+1}$$ 은 $$w_1, .. , w_{l+1}$$ 의 선형 결합이고
- $$u_{l+1} \neq 0$$ 이므로
- $$v_{l+1} = {u_{l+1} \over \|u_{l+1}\|}$$ 로 쓸 수 있다.

## Gram-schmidt에서 꺼낼 수 있는 부가 정리

$$X$$ : inner product space, $$Y$$ : finite dimensional subspace of $$X$$ 라고 하자

$$\{v_1, ... ,v_k\}$$ → $$Y$$의 orthonormal basis

$$x \in X, y \in Y, z\in Y^\perp$$ 일 때

$$x = y+z$$ 로 표현할 수 있고 이때의 $$y,z$$는 유일하다.

**proof**

$$y = \sum_{i=1}^k<v_i,x>v_i \in Y\\
z = x-y \in Y^\perp$$

라고 써보자

$$<v_i,z> = <v_i,x>-<v_i,y>\\
= <v_i,x> - <v_i, \sum_{i=1}^k<v_i,x>v_i>\\
= <v_i,x> - <v_i,x><v_i,v_i> \\
= <v_i,x>(1-<v_i,v_i>) = 0$$

이므로 $$z=x-y \in Y^\perp$$ 가 된다.

또한 위 $$y,z$$에 대한 표현식은 유일해진다. 이를 알아보고자 하는데, 우선

$$y\neq y', z\neq z'$$ , $$y,y' \in Y$$, $$z,z\in Y^\perp$$라고 해보자.(가정)

$$x=y+z=y'+z'\rightarrow y-y'=z-z'$$

$$Y \cup Y^\perp = \{0\}$$ 이므로 $$y=y', z=z'$$ 이 되는데 이는 가정과도 어긋나게 되고 이로서 $$y,z$$ 가 유일하다는 것을 알 수 있다.

# Norm of linear transformation

## Vector space $$(LT(X,Y),R)$$

$$X,Y$$ 는 Norm이 정의된 space이다. $$X \rightarrow Y$$ 인 모든 linear transformation을 모은 set을 생각해보자. 이런 set of linear transformation을 vector space로 살펴보고자 한다. vector space로 살펴보려면 $$+, \cdot$$ 연산을 정의해야한다.

$$L_1, L_2 \in L, \alpha \in R\\
(L_1 + L_2)(x) = L_1(x) + L_2(x) \\
(\alpha L_1)(x) = \alpha\cdot L_1(x)$$

위와 같이 정의한 vector space of linear transformation을 $$(LT(X,Y) R)$$ 라고 적을 수 있다.

## Norm $$(\|A\|)$$

이제 vector space $$(LT(X,Y),R)$$에서 Norm을 정의할 것인데, $$X,Y$$에 norm이 정의되어 있으므로 $$X,Y$$의 norm을 이용해 Linear transformation의 Norm을 정의하고자 한다.

$$T \in (LT(X,Y),R) \\
\|T\| := sup( {\|T(x)\|_Y \over \|x\|_X}) \\
= sup( \|T(x)\|_Y ) \text{ where } \|X\|=1$$

즉 0을 제외한 모든 $$x$$ 에 대해서 $$\|T(x)\| \over \|x\|$$ 비율의 최대가 $$\|T\|$$ 가 된다.

- Notation

    $$\|x\|_X$$ : $$X$$에서 정의된 Norm

    $$\|y\|_Y$$ : $$Y$$에서 정의된 Norm

    $$sup$$ : 상한, 최대

만일 $$X = (R^n,R)$$, $$Y=(R^m,R)$$이면 $$T$$는 matrix $$A \in R^{m\times n}$$으로 쓸 수 있고 $$\|T\| = \|A\|$$로 쓸 수 있다.

### 1-Norm $$\|A\|_1$$

$$\|Ax\|_1 = \sum_{i=1}^m |\sum_{j=1}^n a_{ij}x_j| \\
\leq \sum_{i=1}^m\sum_{j=1}^n|a_{ij}\|x_j| \\ 
\leq \sum_{j=1}^n|x_j|\sum_{i=1}^m|a_{ij}| \\
\leq (\sum_{j=1}^n|x_j|)\cdot (max_j (\sum_{i=1}^m |a_{ij}| )) \\
\leq \|x\|_1 \cdot (max_j (\sum_{i=1}^m |a_{ij}| ))$$

$max_j (\sum_{i=1}^m \|a_{ij}\|)$ 는 $$A$$의 maximum column sum을 구하는 것이다. matrix $$A$$의 column별로 다 더하고, 그 중 가장 큰 값을 return 하는 함수

$$\|A\|_1 = sup {\|Ax\|_1 \over \|x\|_1} \leq max_j (\sum_{i=1}^m |a_{ij}| )$$

과연 $$=$$가 존재하는가 를 알아볼 필요가 있다. 왜냐하면 만일 $$=$$ 가 존재하면 꽤나 tight한 boundary가 되기 때문이다. 

$max_j (\sum_{i=1}^m \|a_{ij}\| )$ 값을 내는 $$j$$ 를 $$j_0$$ 라고 해보자. 

이때 만일 $$i = j_0 \rightarrow x_i=1$$,  $$i\neq j_0 \rightarrow x_i=0$$ 으로 설정하면

$$Ax$$는 $$A$$의 $$j_0$$ 열 만 골라내고, $$\|x\|_1=1$$ 이 되고 $$\|Ax\|_1 = \sum_{i=1}^m\|a_{ij_0}\|=max_j (\sum_{i=1}^m \|a_{ij}\| )$$ 가 된다.