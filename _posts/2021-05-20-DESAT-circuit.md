---
layout: post
title: DESAT 회로
subtitle: Power Switch 과전류를 감지하는 Gate driver의 DESAT 기능에 관하여
date: '2021-05-20 20:59'
categories: ["Gate driver 만들기"]
type: "post"
published: false
---
### 목차
- [DESAT의 목적과 기능](#desat의-목적과-기능)
- [IGBT의 $$I\_c - V\_{CE}$$ 특성](#igbt의-i_c---v_ce-특성)
- [DESAT 기능을 위하여 구현해주어야 할 회로](#desat-기능을-위하여-구현해주어야-할-회로)
    - [1단계 : 내부 DESAT 회로와 Blank Capacitor, DESAT Resistor, DESAT diode 갖추기](#1단계--내부-desat-회로와-blank-capacitor-desat-resistor-desat-diode-갖추기)
    - [2단계 : DESAT회로와 Gate driver를 보호할 다이오드 추가하기](#2단계--desat회로와-gate-driver를-보호할-다이오드-추가하기)
    - [3단계 : 과전류를 탐지할 적절한 $$V\_{CE}$$ 범위 회로로 설정하기](#3단계--과전류를-탐지할-적절한-v_ce-범위-회로로-설정하기)
- [참고문서](#참고문서)

# DESAT의 목적과 기능
3상 모터를 동작하는 Inverter와 같이 대량의 전류를 흘려보낼 파워단 스위치로는 IGBT, MOSFET 등등이 있다. 이러한 스위치에 과전류가 흐르면(실수든, 사고든) 소자가 고장나고 결국 <span style="color:red">불🔥</span>이 난다. 이러한 과전류를 방지하기 위하여 파워 스위치를 구동시키는 Gate driver에 과전류를 탐지하는 여러 기능들이 있는데, 이러한 기능들 중 하나가 **DESAT**이다.

![gatedriver][gatedriver-pinmap]
[<center> UCC21750 Gate Driver Pinmap </center>][UCC21750]

위 그림과 같이 Gate driver에 DESAT이란 핀이 나와 있고, 이러한 핀에 아래에 후술할 회로들을 구성해줌으로서 Gate driver가 고전압이 물려있는 파워 스위치에 과전류가 흐르는 것을 감지할 수 있게 해준다.


# IGBT의 $$I_c - V_{CE}$$ 특성
![iv][ic-vce]
[<center> $I_c-V_{CE}$ curve</center>][ic-vce]

 본 글에서는 IGBT를 Power Switch로 쓴다. G: Gate, C: Collector, E: Emitter이다. $$V_{GE} $$가 threshold보다 높아지고, 전류 $$ I_c $$가 흐르면 $$ V_{CE} $$도 커지게 된다. 스위칭 동작은 위 그래프의 linear region에서 동작하며, 과전류가 흐르면 $$ V_{CE} $$가 따라 커진다.  

DESAT은 바로 이러한 $$V_{CE} $$ 전압을 Gate driver 내부의 기준 전압( $$ V_{DESAT} $$)과 비교하여 $$ V_{CE} $$가 더 크면 과전류가 흐른다고 판단해 fault 신호를 외부에 보낸다.

# DESAT 기능을 위하여 구현해주어야 할 회로
### 1단계 : 내부 DESAT 회로와 Blank Capacitor, DESAT Resistor, DESAT diode 갖추기

![ckt1][DESAT-ckt]
[<center> UCC21750의 DESAT 회로(DATASHEET Figure46, page 30) </center>][UCC21750]

VDD와 연결된 Transformer 기호는 DESAT 핀으로 전류를 쏴주는 전류원 역할을 한다. 현재 DESAT 상태인지 아닌지 내부에서 판단하는 **기준전압인 $$ V_{DESAT} $$**과 비교기 comparator가 있고, $$ V_{DESAT} $$은 일반적으로 9V이다. 입력 값이 이 기준전압보다 큰 지 아닌지 판단하고 fault signal을 낸다.  

내부에 있는 Pull down P형 MOSFET은 DESAT이 연결된 스위칭 소자가 turn on 될때에만 DESAT이 동작할 수 있도록 한다. 연결된 IGBT가 꺼지면 P형 모스펫이 켜짐으로써 $$ C_{BLK} $$에 쌓여있는 전하를 방전시키는 역할을 한다. 즉 DESAT을 초기화 시켜주는 작업을 한다.

본 문서에서는 아래의 그림과 같이 Gate Driver가 윗상 IGBT의 과전류를 탐지하는 시나리오를 다루고 있다. 

![ckt1][ckt-1]

1. 윗상 스위치가 켜지면 윗상의 Emitter가 Collector로 붙게 되고, $$ V_{CE} $$가 줄어들게 되고 최종적으로는 turn on voltage(커봐야 2-3V? 정도..? 정확한 값은 소자에 따라 다르다)를 유지하게 된다.
2. 내부의 전류원으로 인해 $$ C_{BLK} $$ 충전되면서 DESAT핀의 전압(capacitor 양단의 전압)이 올라가겠지만, $$ V_{CE} $$ 가 turn on voltage를 유지하고 있는 상태에서 $$ C_{BLK} $$ 의 양단 전압이 더 커져 $$ V_{CE}+V_{f,diode} $$가 되면 $$ C_{BLK} $$ 는 더 충전되지 않고 전류는 diode를 지나 IGBT로 나가게 된다. 만일 과전류가 흐르고 있다면 $$ V_{CE} $$가 크므로 capacitor 양단의 전압이 $$ V_{DESAT} $$보다 커지게 될 것이다.

3. 그런데 이때 스위치가 켜지는 바로 그 순간을 살펴보면 $$ V_{CE} $$는 $$ V_{DC} $$에 가깝다. 만일 $$ C_{BLK} $$가 작아서 $$ V_{CE} $$가 줄어드는 속도보다 더 빨리 충전되어버린다면 과전류가 아닌 상황임에도 불구하고 Gate driver는 과전류 상태로 인식되어버리는 상황이 된다. 한편 $$ C_{BLK} $$가 또 너무 크면 IGBT가 과전류를 견딜 수 있는 최대 시간이내로 $$ C_{BLK} $$를 충전하지 못해 Gate driver가 과전류 상황을 알아차리기 전에 소자가 🔥타버릴 수 있다. 따라서 $$ C_{BLK} $$를 적절한 값으로 설정해야 하며 다음과 같이 고려해볼 수 있다.  

![toshiba-desat][toshiba-desat]

$$ 
 t_{BLANK} = C_{BLK}\times { (V_{DESAT} - (V_F + I_{CHG\times R_{DESAT}})) \over I_{CHG} }
$$

[<center> TOSHIBA의 Smart Gate Driver Coupler Tips for Designing DESAT Detection Circuits </center>][Smart Gate Driver Coupler Tips for Designing DESAT Detection Circuits]

$$ t_{BLANK} $$가 소자의 $$ V_{CE} $$ 가 줄어드는 시간보다는 커야하며 소자가 과전류를 견딜 수 있는 시간보다는 짧아야 한다.  

**저항은 왜 있는 것일까?**  
Gate driver 내부 전류원에 한계가 있다. 따라서 출력 전류를 제한할 필요가 있는데, 이를 $$ R_{DESAT} $$이 해준다  

**Diode는 왜 있는 것일까?**  
역전류를 방지하기 위함이다. 가령 LOAD에서 회생제동처럼 발전을 하고 있다고 생각해보자. 그러면 IGBT 내부에 달려있는 diode(freewheeling diode)를 통해서 전류가 흘러들어올 것이다. 이 경우 $$ V_{CE} < 0 $$ 인 상태가 되는데 다이오드가 없다면 거꾸로 전류가 들어올 수 있다. 이러한 회생 제동은 직류가 아니므로 사실 $$ C_{BLK} $$ 를 통해서도 들어오는데, 이를 막기 위한 추가적인 다이오드가 필요하다. (후술)

### 2단계 : DESAT회로와 Gate driver를 보호할 다이오드 추가하기
**Positive Voltage Protection: Zener diode**  
![ckt2][ckt-2]
위 그림의 빨간색으로 그려진 Zener diode가 capacitor 양단 전압을 제한한다.  

Gate driver 내부에는 전류원만 있지 capacitor 양단 전압을 제한해주지는 않는다. 만일 외부 IGBT가 short circuit이 되었고, $$ V_{CE} $$가 계속 큰 값을 유지하면서 $$ C_{BLK} $$가 충전되는 상황에서 IGBT를 끄기 전에 capacitor 양단 전압이 capacitor 내압 전압보다 커진다거나 Gate driver를 파괴하기에 충분한 전압이 될 수도 있다. 따라서 전압의 상한값을 제한해줄 필요가 있다. Zener diode가 그런 역할을 해주며, reverse break down voltage가 걸리면 그 전압을 유지한 채 전류가 거꾸로 흐르게 되어 전압이 증가하지 않도록 막는다. 다시 capacitor 양단 전압이 다시 낮아져 reverse break down voltage보다 낮아지면 Zener diode는 정상적으로 돌아온다.

**Negative Voltage Protection: schottky diode**  
![ckt3][ckt-3]

LOAD에서 발전을 한다거나 해서 $$ V_{CE} $$가 역전되면 capacitor에 Negative 전압이 걸리고 $$ C_{BLK} $$를 타고 전류가 들어오게 된다. 이는 Gate driver에 손상을 줄 수 있다. 이를 방지하기 위해 schottky diode를 capacitor에 병렬로 연결하여 Negative voltage를 방지하게 한다. schottky diode를 쓰는 이유는 일반적으로 schottky diode가 반응 속도가 빨라서이다.

### 3단계 : 과전류를 탐지할 적절한 $$V_{CE}$$ 범위 회로로 설정하기

드라이버의 DESAT reference voltage는 바꿀 수가 없다. DESAT reference voltage가 큰 이유는 다양한 IGBT를 대응하기 위함이다. 어떤 IGBT는 과전류가 흐를 때 $$ V_{CE} $$ 가 5V일 수도 있고, 어떤 IGBT는 과전류가 흐를 때 8V일 수도 있다. reference voltage와 비교할 전압 값이 과전류가 흐를 때 9V를 넘어야 하므로 다양한 IGBT에 대해 대응하기 위해서는 아래와 같이 voltage source가 있으면 편하다.

![ckt4][ckt-4]
<center> DESAT diode 옆에 잘 보면 Voltage source가 붙어있다. </center>

실제로 voltage source를 붙이지는 않고 저 위치에 diode를 추가로 직렬로 연결하여 조절한다. 만일 IGBT가 과전류일 때 $$ V_{CE} $$가 5V이고 DESAT reference voltage가 9V이면 forward voltage, $$ V_{F} $$가 2V인 다이오드(가령 [US1NWF-7][US1NWF-7])를 2개로 직렬 연결하면 $$ V_{CE} $$가 5V가 될 때 comparator에서는 9V+alpha( $$ V_{resistor} $$) 이 들어가게 된다

# 참고문서
- [[파워 일렉트로닉스] 고내압, 대전류를 ON/OFF하기 위한 파워트랜지스터 IGBT의 기초](http://magazine.hellot.net/magz/article/articleDetail.do;jsessionid=2177DE65DBDF538ED78DF65DE83FA277?flag=all&showType=showType1&articleId=ARTI_000000000030212&page=1&articleAllListSortType=sort_1&selectYearMonth=201409&subCtgId=)
- [STMicroelectronics, IGBT datasheet tutorial, page14, figure 10](https://www.st.com/resource/en/application_note/dm00122161-igbt-datasheet-tutorial-stmicroelectronics.pdf )
- [infineon, IGBT diagram](https://www.infineon.com/cms/en/product/power/igbt/igbt-discretes/ikw25n120h3/)
- [Smart Gate Driver Coupler Tips for Designing DESAT Detection Circuits][Smart Gate Driver Coupler Tips for Designing DESAT Detection Circuits]
- [UCC21750DW datasheet][UCC21750]
- [US1NWF-7 datasheet][US1NWF-7]
- [스마트 게이트 드라이브 옵토커플러의 UVLO, DESAT 탐지 기능 시뮬레이션](http://www.hellot.net/new_hellot/magazine/magazine_read.html?code=202&sub=&idx=21166&page=&list=)


[Smart Gate Driver Coupler Tips for Designing DESAT Detection Circuits]:https://toshiba.semicon-storage.com/info/docget.jsp?did=66192
[US1NWF-7]:https://www.diodes.com/assets/Datasheets/US1NWF.pdf
[UCC21750]:https://www.ti.com/lit/ds/symlink/ucc21750.pdf
[gatedriver-pinmap]:/assets/images/deset-circuit/ucc21750dw.png
[IGBT-sym-ref]:https://www.infineon.com/cms/en/product/power/igbt/igbt-discretes/ikw25n120h3/
[IGBT-sym]:https://lh3.googleusercontent.com/pw/ACtC-3df_D7AxcayRnpEIZ9EyL2BP88S6Ar3uO_9cJklcAbJ7AIv8dd8Xqx78AVKYWgZDQRD3gMs06QBgYbcyv9-wb9B0hekrw6xZ3uQn6kaerGXesMWD8PuseBkBG0uebwE-XFM_cYGXmx60e0AZE5BGANjFg=s367-no?authuser=2 
[ic-vce]:/assets/images/deset-circuit/Ic-Vce.png
[ic-vce-ref]:https://www.st.com/resource/en/application_note/dm00122161-igbt-datasheet-tutorial-stmicroelectronics.pdf
[DESAT-ckt]:https://lh3.googleusercontent.com/pw/ACtC-3d8JPJW3w69U48359ajHgoI-4Ps_yOMa0UUeOKjqYWkZSK3r6zFC5uZF7awFVQFCUdimNihHz4qdKDL_u0FvbR0a8PApCpWW2F3NGJzAYAnqO1BfaEyPSDWufMZE1cWeR-ZckjdxKyngfEFOBOgWffZJA=w602-h300-no?authuser=2

[ckt-1]:https://lh3.googleusercontent.com/pw/ACtC-3foQTAx8SEMS9S5G8C9yp8HJ8hIakhCCcwpZjdNwqs7b0wTc-yeQNa78ieKbi1GdNMQQljdXFndvi3NsQcbkNeUCI-7Q8JGrkzrGqPPsKGtNj0a7kXY_LkJAa0iXlr-_fLv8m2f42mA0FOTyZRoEcAuew=w613-h343-no?authuser=2
[ckt-2]:https://lh3.googleusercontent.com/pw/ACtC-3fvSp72FrMBpVYV3NN11bwdWCm7XhjevrWkfOIBs98ZdIKD-0Gx4wsBj4uZFDnbIJSFC5PjvHC_QlrG-LM0HHAa0bcIH7qb-c40sIXrQjBHXRdPwGTGOohAne4HUfRV-vo0pC2xsi_aX6MDkufw1Zgk9Q=w602-h349-no?authuser=2
[ckt-3]:https://lh3.googleusercontent.com/pw/ACtC-3cFJ7zcL6jPLOJ5yDWCGYwa8bifmOcYR9uGJsNZaDcYVJADXTGko2evjt1eD_hRHtpLy2QMUxzH_kEw7W-LB2Vmj2xvL01kvpejFxY5yK_aKGXMq2yjQlL8tMD7PUXC85sis83eXPo-lr2C63CzoUOqRw=w602-h359-no?authuser=2
[ckt-4]:https://lh3.googleusercontent.com/pw/ACtC-3ckMWADpEt9iZ513AQkQdB05U2inl3ECCXjITNVJCB07oVL9_zuMrGBlWem8Ps24hgQtiMhc8-rEECkloAKv7vHmJy_z0Y4XI9HYlbXiaAhB1LSBWpFVZ28NfGbYnluVCmOdQ7eDPuQ64K-oy-GeHMA6w=w602-h358-no?authuser=2
[toshiba-desat]:https://lh3.googleusercontent.com/pw/ACtC-3cMrl0L0LIxpE4y48fTNDsh2NgObpoVeYKOkejSO7AhfO_HBWn36fxqvsJin_EVCBqPJ3j7CIEQHjLF6dTVuWIe1_Hu6wGco6t6nKifMELJu6Yg0zPkeQt5Phc2SLp5SYDKLFc3r0Ivz3sfk5_mnivg_w=w645-h285-no?authuser=2