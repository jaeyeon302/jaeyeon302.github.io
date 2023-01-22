---
layout: post
title: DESAT 회로 구성하기
subtitle: 실제 Gate Driver의 DESAT 주변 회로 구성하기
date: '2021-06-21 20:59'
categories: ["Gate driver 만들기"]
type: "post"
published: false
---
### 들어가기에 앞서
근래 3상 Inverter를 만들고 있는데, 스위칭 소자는 [CREE 사][cree]의 [CAB011M12FM3][CAB011M12FM3 datasheet]를 쓰고 있고, Gate driver로는 [Texas instruments 사][ti]의 [UCC21750][UCC21750 datahsheet]를 사용하고 있다. 링크된 글을 제외하고 본 글에서 다루고 있는 Gate driver와 스위칭 소자는 위 두 제품을 기준으로 하고 있다.


### 목차
- [DESAT 회로 구성에 필요한 정보](#desat-회로-구성에-필요한-정보)
- [DESAT을 구성하기 위해 데이터시트에서 봐야할 것](#desat을-구성하기-위해-데이터시트에서-봐야할-것)
    - [몇 A가 흐를 때 스위칭 소자가 최대 몇 초까지 견딜 수 있는가? : SOA](#몇-a가-흐를-때-스위칭-소자가-최대-몇-초까지-견딜-수-있는가--soa)
    - [스위칭 소자가 켜졌을 때 $$V\_{DS}$$의 정상범위는 몇 V인가?](#스위칭-소자가-켜졌을-때-v_ds의-정상범위는-몇-v인가)
    - [스위칭 소자가 켜졌을 때 $$V\_{DS}$$가 몇 초 이내로 정상 전압으로 수렴하는가?](#스위칭-소자가-켜졌을-때-v_ds가-몇-초-이내로-정상-전압으로-수렴하는가)
- [DESAT 주변 회로 구성하기](#desat-주변-회로-구성하기)
    - [1. 스위칭 소자가 켜졌을 때 $$V\_{DS}$$가 줄어드는 속도](#1-스위칭-소자가-켜졌을-때-v_ds가-줄어드는-속도)
    - [2. 스위칭 소자가 과전류를 견딜 수 있는 최대 시간](#2-스위칭-소자가-과전류를-견딜-수-있는-최대-시간)
    - [3. 정상 동작 중 $$V\_{DS}$$](#3-정상-동작-중-v_ds)
    - [4. 결론](#4-결론)
- [참고문서](#참고문서)


# DESAT 회로 구성에 필요한 정보
DESAT에 대한 설명은 [DESAT 회로][DESAT 회로 페이지]에서 다룬다.  
DESAT은 기본적으로 스위칭 소자의 단락사고를 방지하기 위한 기능이다.  
이러한 기능을 효과적으로 동작시키려면, 스위칭 소자를 적절한 시간 내에 꺼야한다. 정상 동작 중에 DESAT의 오작동으로 스위칭 소자를 끄지 않기 위해서는 스위칭 소자가 켜질 때 $$V_{DS}$$가 충분히 줄어들고 난 뒤 동작해야하며, 스위칭 소자가 과전류를 견딜 수 있는 최대 시간 이내에 동작해야 한다.

이러한 적절한 시간을 알기 위해서 사용하고자 하는 스위칭 소자의 datasheet를 살펴볼 필요가 있다. 
datasheet를 통해 알아야할 정보로는 다음과 같은 것들이 있다.
1. 몇 A가 흐를 때 스위칭 소자가 최대 몇 초까지 견딜 수 있는가?
2. 스위칭 소자가 On 된 후 $$V_{DS}$$는 몇 V가 정상 전압인가?
3. 스위칭 소자가 On 될 때 $$V_{DS}$$가 몇 초 이내로 정상 전압으로 수렴하는가?

# DESAT을 구성하기 위해 데이터시트에서 봐야할 것

### 몇 A가 흐를 때 스위칭 소자가 최대 몇 초까지 견딜 수 있는가? : SOA
SOA는 Safe Operating Area의 약자이며, 스위칭소자가 안전하게 동작할 수 있는 전압, 전류 조건을 보여주는 그래프이다. Forward Bias SOA(*FBSOA*) 있고, Reverse Biase SOA (*RBSOA*) 가 있다. 
- **FBSOA**
  : 스위칭 소자가 켜졌을 때 각 전압, 전류 조건에서 손상 없이 견딜 수 있는 시간을 보여준다
- **RBSOA**
  : 스위칭 소자가 꺼졌을 때 각 전압, 전류 조건에서 손상 없이 견딜 수 있는 시간을 보여준다.

  DESAT 회로는 스위칭 소자가 켜졌을 때 과전류로 인한 소자 손상을 방지하기 위함이므로 데이터시트에서 FBSOA를 보면 된다. DESAT 회로의 Capcaitor가 FBSOA에서 정해진 안전운전 시간이내에 충분히 충전되어야 Gate driver 내부의 DESAT Comparator가 과전류 여부를 판단할 수 있다.

### 스위칭 소자가 켜졌을 때 $$V_{DS}$$의 정상범위는 몇 V인가?  
이는 데이터 시트의 **$$I_{DS} - V_{DS}$$** 그래프를 보면 된다. 여기서 $$I_{DS}$$는 Drain에서 Source로 흐르는 전류의 양을 의미하고, $$V_{DS}$$는 Drain과 Source 사이의 전압을 의미한다. 이를 이용해 DESAT 회로의 diode의 forward bias를 어떻게 잡을지 결정할 수 있다.

### 스위칭 소자가 켜졌을 때 $$V_{DS}$$가 몇 초 이내로 정상 전압으로 수렴하는가?  
이는 $$ {dV_{DS} \over dt} $$ 그래프를 보면 된다. 스위칭 소자의 온도에 따라 Drain - Source 사이 전압이 줄어드는 시간이 다르다. DESAT 회로는 $$V_{DS}$$가 정상 전압으로 수렴한 뒤 동작해야한다. 즉 DESAT 회로의 Capacitor가 $$V_{DS}$$가 정상적으로 줄어들고 있는 시간 이내에 충분히 충전되면 안된다. ( DESAT Comparator의 reference voltage보다 전압이 올라가면 안된다는 뜻)

DESAT 회로가 동작을 시작하기까지(Comparator 9V가 비교를 시작하는 순간까지)의 시간이 $$V_{DS}$$가 줄어드는 시간의 가장 긴 시간보다 길어야 한다.


# DESAT 주변 회로 구성하기
[CREE 사][cree]의 [CAB011M12FM3][CAB011M12FM3 datasheet]를 기준으로 주변 회로는  다음의 절차를 거쳐 구성해보았다.

### 1. 스위칭 소자가 켜졌을 때 $$V_{DS}$$가 줄어드는 속도
   ![ds_def][datasheet_def]
   <center> CAB011M12FM3 datasheet definitions </center>

   우측 상단 'Turn-on Transient Definitions'를 보면 스위칭 소자가 켜질 때 $$V_{DS}$$가 줄어드는 속도인 $$dv/dt$$  를 정의하고 있다.  
    
   ![ds_dvdt][datasheet_dvdt]
   위의 그래프는 Juntion 온도에 따른 $$dv/dt$$를 보여주고 있다. 우리가 보고자 함은 $$dv/dt_{on}$$ 이며 본 소자가 견딜 수 있는 최대 온도 150도에서 Drain-Source 전압이 떨어지는 속도가 제일 느린 것을 볼 수 있다. DESAT 회로는 최소한 30ns 이후에 동작해야 함을 알 수 있다.

### 2. 스위칭 소자가 과전류를 견딜 수 있는 최대 시간
   ![ds_FBSOA][datasheet_FBSOA]
   $$V_{DS}$$ 500V 기준으로 50A 10us를 최대한 견딜 수 있다. (시간 축이 log scale임에 유의) 내가 만들고자하는 Inverter는 Peak 100A까지를 고려하고 있다. 따라서 위 1에서 정한 30ns 직후 Capacitor 양단에 걸리는 전압이 DESAT Comaparator의 reference voltage보다 높아져 DESAT이 잡히도록 하면 스위칭 소자를 가장 보수적으로 운용할 수 있을 것이다. (약간의 위험도 감수하지 않겠다는 뜻)

### 3. 정상 동작 중 $$V_{DS}$$
   ![ds_VDS][datasheet_VDS]
   175도 기준 100A가 흐르면 대략 1.7V ~ 2V까지 $$V_{DS}$$가 올라간다.

### 4. 결론
   1) 100A Peak일 때 Drain source voltage 정상 범위는 1.7V ~ 2V이다.
   2) 스위칭 소자가 정상적으로 켜지면 $$V_{DS}$$가 500V에서 1.7V까지 $$25V/1ns$$ 속도로 전압이 줄어들 것이므로 30ns 정도 이후 DESAT이 동작하면 된다.
   3) DESAT Comparator reference voltage가 9V이므로 다이오드를 이용해 7.3V를 만들어 주고 $$T_{blank}$$ 를 50ns 정도로 잡으면 DESAT은 안전하게 소자를 보호할 수 있을 것이다.
   
   Gate driver의 DESAT을 위한 전류원은 500uA 이므로 다음과 같이 DESAT Capacitor를 결정할 수 있다.

   $$ 500uA = C\cdot {\Delta V \over \Delta t} \\
      \Delta V = 9V \\
      \Delta t = 50ns \\
      \therefore C = 3pF
   $$

   3pF 이면 50ns, 6pF이면 100ns, 12pF 이면 200ns 로 $T_{blank}$를 결정할 수 있다.
   위 과정을 거쳐 결정된 DESAT 회로는 다음과 같다.

   ![circuit][circuit]




   


# 참고문서

- [ROHM-트랜지스터 안전하게 사용하기][ROHM-트랜지스터 안전하게 사용하기]
- [CAB011M12FM3 datasheet][CAB011M12FM3 datasheet]
- [UCC21750 datahsheet][UCC21750 datahsheet]
- [Toshiba - What is a safe operating area?][What is a safe operating area?]

[What is a safe operating area?]:https://toshiba.semicon-storage.com/kr/semiconductor/knowledge/faq/mosfet_igbt/igbt-008.html
[UCC21750 datahsheet]:https://www.ti.com/lit/ds/symlink/ucc21750.pdf?ts=1624244172739&ref_url=https%253A%252F%252Fwww.google.com%252F
[ti]:https://www.ti.com/ko-kr/homepage.html
[CAB011M12FM3 datasheet]:https://www.richardsonrfpd.com/docs/rfpd/CAB011M12FM3.pdf
[cree]:https://www.cree.com/
[ROHM-트랜지스터 안전하게 사용하기]:https://www.rohm.co.kr/electronics-basics/transistors/tr_what6
[UCC21760]:https://www.ti.com/product/UCC21750
[DESAT 회로 페이지]:/gate%20driver%20만들기/2021/05/20/DESAT-circuit.html

[datasheet_def]:https://lh3.googleusercontent.com/pw/ACtC-3e8dtexA_YN7fuWb0Mk84z0cMldPkWytGaLnDdqfT5Vn0RvPC8PuKB-jdt0tfzIOqajRq7JQ2ZvHlHqxF-H-vcLlD6EeqLuDh3Cg60nYuWMPWY-adQJIBY1tMUMyuv50ivM9N90cYNEeqYIKvWB6d0oIQ=w1487-h1197-no?authuser=1
[datasheet_dvdt]:https://lh3.googleusercontent.com/pw/ACtC-3ceZfPGKaivhHDHZPN0xFgKLo2qs2NkOOJoyy9CTjd54mckq8xwb_6cmCz2oyyo2wWws2c9LEfVgZiDpzahgKMLK_gGHQu8813oQjz2IMcIEoRP70Lp3zzRIaKMA-twBwRxzIMTcfzYeUhJxPdYc9MUzg=w750-h574-no?authuser=1
[datasheet_FBSOA]:https://lh3.googleusercontent.com/pw/ACtC-3ccnY0dHsYZvKKoxuTfzR7xhroqp9OUnDPi1_WRmyqwrohUHi2XAN4Zi0xnLyO_NN0A4wbK3I7gXnuzj4P1VT7NAN31A9VcJqKrQN2YhThporEwLmZfwZ1PyMyHZLSfdqpz-LzhZP0c2FFXoXtPSdxA5A=w719-h573-no?authuser=1
[datasheet_VDS]:https://lh3.googleusercontent.com/pw/AM-JKLWJ-F-hloWZxn5-Kh0DeCKzdLKwPrBVyLWa-N2E6A6Z6JJnS3Fag8VK9uIYlhH2WtxOjXRZNIaYUdk8M6AgW-fVYP2BJ58dyA-FAHc_8xlAP0GAXhVVFUuin717__qOmtGK1MOVTG4xL5CZ8kzT-nRH9A=w760-h627-no?authuser=1

[circuit]:https://lh3.googleusercontent.com/pw/AM-JKLWu90GNGzA0WqEHzx3spyckBGNGtSLtHomYvUmFWTdPlj0y4WPiW03QwQa8INC1NGa1g9rYRYHKxTkIrbZgXgNNM-3-8qj7LOGmcdQSNplFYdt69K-1EzS2A2ILyQHlAoGWGt7bWvRx2KOcwt8g7sGrEA=w2874-h714-no?authuser=1