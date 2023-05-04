---
layout: single
title: "[데이터통신] 5장 Signal Encoding Techniques"
excerpt: "5장 Signal Encoding Techniques"
date: 2021-05-01T00:00:00+09:00
toc: true
toc_sticky: true
use_math: true
categories:
  - 전공
  - 데이터통신
tags:
  - 전공
  - 데이터통신
---

- 원래의 신호는 전송에 적합한 형태가 아님
→ 전송에 적합한 형태로 바꾸기 위해 인코딩을 함
- 인코딩 4가지 방식
    - 디지털 데이터 → 디지털 신호
        - 가장 단순한 형식
        - 하나의 전압 레벨을 1에 할당하고 다른 전압 레벨은 0에 할당
        - 더 복잡한 인코딩 scheme이 신호의 스펙트럼을 변경시키는 것에 의해 성능을 향상시키기 위해 사용됨
    - 디지털 데이터 → 아날로그 신호
        - 음성을 사용하기 위해 사용
        - 모뎀을 이용해서 디지털 데이터를 아날로그 신호로 바꿈
        - Aplitude shift keying(ASK)
        - Frequency shift keying(FSK)
        - Phase shift keying(PSK)
    - 아날로그 데이터 → 디지털 신호
        - 음성이나 비디오 같은 아날로그 데이터를 디지털 전송장비를 사용하기 위해 디지털로 바꿔야함
        - 가장 간단한 기술은 pulse code modulation(PCM)
        - PCM을 하기 위해서는 sampling을 해야함
        - 아날로그는 점의 연속이므로 이것을 다 샘플링하면 데이터가 엄청 많아짐
        → 몇가지 점만 샘플링해서 디지털 값으로 바꿈
        - 샘플링하는 점의 간격을 어떻게 할지?
            - 간격이 좁을수록 복원이 정확해짐
            - But 데이터량이 많음
            - 사용할 수 있는  대역폭과 속도가 제한되어 있으므로 제한된 속도와 시간 안에 전송해야 함
    - 아날로그 데이터 → 아날로그 신호
        - 아날로그 전송 시스템을 사용하기 위해 다른 주파수 대역으로 이동 시킴
        - Amplitude modulation(AM)
        - Frequency modulation(FM)
        - Phase modulation(PM)
- 아날로그와 디지털 정보 모두 아날로그 또는 디지털 신호로 부호화될 수 있다.
- 선택되어진 특정한 인코딩이란 것은 특정한 요구사항에 의존적이다.
    - 미디어에 따라 인코딩 방식이 달라진다.
    - 이용 가능한 통신 설비가 어떤 것인지에 따라 인코딩 방식이 달라진다.
    
- 데이터를 디지털 신호로 바꿔서 전송할 때 필요한 것 : Encoder
- 수신측에서 원래 신호로 복원할 때 사용하는 것 : Decoder

- 데이터를 아날로그 신호로 바꿔서 전송할 때 필요한 것 : Modulator
- 수신측에서 원래 신호로 복원할 때 사용하는 것 : Demodulator
    - 반송 주파수(carriere frequency)사용하여 전송
    - 신호가 반송 주파수를 중심으로 분포
    - 반송 주파수를 달리하면 다른 쪽으로 이동, 폭은 동일

## 디지털 데이터 → 디지털 신호

- 디지털 신호
    - 이산적이고 불연속적인 전압
    - 표현공간이 제한적
    - 각각의 펄스가 하나의 신호 요소가 된다.
    - 이진 데이터가 신호 요소로 인코딩된다.

#### 용어

- Unipolar : 모든 신호 요소가 같은 부호를 갖는다. 0V, 5V
- Bipolar : 하나의 논리 상태가 양의 전압을 나타내고 다른 하나가 음의 전압을 나타냄 +5V, -5V
- Data rate(전송 속도)
    - R로 표현
    - 1초에 전송할 수 있는 비트의 수
    - bps 단위 시간 당 전송할 수 있는 비트의 수
- Duration or length of a bit
    - 한 비트의 폭
    - duration과 data rate는 역수 관계 1/R
- Modulation rate
    - D라고 표현
    - 단위 : baud = signal element/s
- Mark and space
    - mark : 1인 상태
    - space : 0인 상태

#### Interpreting Signals

- 수신측에서 신호를 해석해야 함
- 해석을 잘하려면
    - bit의 타이밍을 알아야함
        - 언제 한 비트가 시작하고 끝나는지 알아야 함(동기화 문제)
    - 신호의 레벨이 일정 수준 이상이면 1, 이하이면 0
- 신호 해독에 영향을 미치는 것
    - snb(signal to noise)가 높을수록 좋은 퀄리티
    - 전송 속도가 빠를수록 에러 날 확률이 높음
        - 전송 속도가 빠를수록 한 비트가 가지는 에너지가 적어짐
        → 미약한 노이즈에도 영향을 받을 수 있음
    - 대역폭이 클수록 신호 전달률이 뛰어남
    - Encoding scheme

#### 디지털 신호 인코딩 형식

###### Nonreturn to Zero-Level(NRZ-L)

- 0이면 high level
- 1이면 low level

###### Nonreturn to Zero Inverted(NRZI)

- 비트의 시작점에서 천이의 여부에 따라 0,1이 결정
- 0이면 그대로
- 1이면 천이
- Differential encoding 방식
    - 레벨 감지보다 신뢰성이 높음
    - 에러 발생 확률 낮음
    - 노이즈 영향 받지 않음
    - 천이가 일어나는 것을 노이즈가 바꿔놓을 수 없음

###### Bipolar-AMI

- 1일 때 positive와 negative를 왔다갔다 함
- bipolar 방식

###### Pseudoternary

- 0일 때 positive와 negative를 왔다갔다 함
- bipolar 방식

###### Manchester

- 각 비트의 중간에서 천이가 일어남
- 천이 방향이 중요
    - 1일 경우 천이가 위로 일어남
    - 0일 경우 천이가 아래로 일어남
- 동기화 능력이 있음
- 단점 : 큰 대역폭을 요구
- But 동기화가 되기 때문에 이 방식을 많이 사용함

###### Differential  Manchester

- 각 비트의 중간에서 천이 발생
- 0이 나올 때만 천이 발생
- Differential encoding 방식

## Encoding Schemes

- 인코딩 방식 성능 평가 필요
- 성능을 비교하는 기준
    - Signal spectrum(신호가 가지는 주파수의 분포)
        - 주파수를 많이 포함하면 전송하기 적합하지 않음
        - 주파수의 대역폭을 작게함
    - Clocking(동기화 능력)
        - Manchester, Differential Manchester
            - Signal spectrum관점에서는 안좋음
    - Error detection(에러 감지 능력)
        - Bipolar-AMI, Pseudoternary, Manchester, Differential Manchester
    - Signal interference and noise immunity(신호 간섭, 잡음)
        - NRZI
        - Differential encoding방식은 천이 감지 방식이므로 잡음에 강함
        → 에러가 일어날 확률 적음
    - cost and complexity
        - 복잡도가 높으면 가격이 높음
        - Signaling rate가 높을수록 가격이 높음

#### Nonreturn to Zero

- 레벨 감지
- 비트의 중간에서 신호의 세기가 크면 0, 작으면 1
- 가장 쉬운 방식 → 일반적으로 많이 사용
- 하나의 볼트의 duration동안에는 천이가 발생하지 않음
- 0일 때는 전압이 없고(0V), 1일때는 양의 전압(5V)
    - 거꾸로 되는 경우도 있음

#### Nonreturn to Zero Inverted(NRZI)

- 1이 시작될 때만 천이함
- 각 비트의 기간동안에는 일정
- 비트의 시작점에서 천이 여부에 따라 천이가 일어나면 1, 일어나지 않으면 0
- Differential encoding 방식 → 신뢰성이 높음
    - 천이는 노이즈에 의해 바뀌지 않음
    - 거꾸로 해도 극성이 바뀌지 않음

###### NRZ 장단점

- 장점
    - 쉽다
    - 대역폭을 효율적으로 사용 → 스펙트럼의 분포가 좁다
- 단점
    - 직류 성분이 존재
    - 동기화 능력이 없다.
    
- 더 많은 bandwidth를 요구하면 바람직하지 않음
- Normalized frequency : f/R 1Hz/1bps = 1 클수록 더 많은 bandwidth 필요

#### Multilevel Binary Bipolar-AMI

- 0일 때는 0, 1일 때는 positive와 negative가 교대적으로 나옴
- 1이 반복될 때는 동기화 능력을 잃지 않음 ← 항상 재동기화 할 수 있는 기회가 주어지기 때문
- 0이 길게 반복될 땐느 동기화 능력을 잃을 수 있음
- 장점
    - 직류 성분이 없다.
        - 신호에서 직류 값은 신호의 평균값
        - 이 방식은 평균값이 0
    - 대역폭을 적게 요구
    - 부분적인 에러를 감지할 수 있는 능력이 있다.

#### Pseudoternary

- 0에 대해서만 positive, negative를 왔다갔다 함
- AMI와 통계적인 성질은 같음

###### Multilevel Binary Issues

- 0, +1, -1 : 레벨이 3개임 → 비효율적
    - 레벨이 3개일 경우 1.58비트를 표현할 수 있지만 1비트를 표현하므로 비효율적
    - 정보를 0.58만큼 손해 봄
- 노이즈에 민감 → 에러가 많이 발생
    - 똑같은 error rate를 이루려면 신호의 품질이 3dB정도 좋아야 한다.
- Energy/Noise 클수록 좋음

#### Manchester Encoding

- 대역폭을 많이 요구 ← 항상 각 비트의 중간에서 천이가 일어나기 때문
- 송신기와 수신기 사이의 동기화 능력을 제공
- 천이 방향 중요
- low → high : 1
- high → low : 0
- 장점 : 동기화
- 단점 : 넓은 대역폭

#### Differential Manchester

- Manchester와 같음
    - 동기화 능력
    - 넓은 대역폭 요구
- But 천이 유무에 따라 0,1 구분
- 0이 시작할 때는 천이, 1이 시작할 때는 천이 X

###### Biphase 장단점

- 장점
    - 동기화 능력이 있다.
    - 직류 성분이 없다.
    - 에러 감지 능력이 있다.
- 단점
    - 각 비트의 중간에서 2번도 천이가 일어남
    - NRZ에 비해 대역폭을 2배 요구

###### Normalized Signal Transition Rate

- data rate/modulation rate
- data rate(bps)
- modulation rate(baud = signal elements/sec)
- 적을수록 효율적
- 적은 대역폭 요구

#### Scrambling

- 동기화 능력을 가져야 함
- But 대역폭 손해
- 자원이 정해지고 자원이 가지고 있는 대역폭이 있음 그 대역폭을 최대로 이용해야 함
→ 전송 속도를 최대로 높이는 것
- Manchester방식은 바람직하지 않음(2배의 대역폭 요구)
⇒ Scrambling 방식 : 동기화 방식을 제공하면서 높은 대역폭을 요구하지 않음
- 동기화 능력을 잃어버리는 이유 : 일정한 레벨이 계속되기 때문
- Scrambling 방식 : 동기화 능력을 잃지 않기 위해 다른 약속된 코드로 바꾸는 것
- 일정한 레벨을 유지할 때 미리 약속된 코드로 바꾸어 놓는데 그 코드는 동기화 능력을 갖기에 충분해야 함
- 송신기와 수신기는 원래의 데이터에서 바뀐 것을 알 수 있어야 함
- 길이는 원래 데이터와 같아야 함

###### 설계 목표

- 직류 성분을 가지지 않는다.
- 동기화 능력을 갖추기 위해 일정 비트 수 이상의 0이 반복되어서는 안된다.
- 전송속도를 희생해서는 안된다. ⇒ 전송속도가 감속되면 안된다.
- 에러를 감지할 수 있는 능력을 가져야 한다.

###### B8ZS

- 8비트의 0이 반복될 때 다른 비트 패턴으로 바꾸는 것
- 000+-0-+
    - 8개의 비트가 모두 0이면 발생
    - 마지만 전압 펄스가 양의 값일 경우
- 000-+0+-
    - 8개의 비트가 모두 0이면 발생
    - 마지막 전압 펄스가 음의 값일 경우

###### HDB3

- 4비트의 연속된 0을 다른 비트 패턴으로 바꾸는 것
- 000-
    - 앞에 있는 펄스가 -
    - 대치 후 앞에 있는 1의 개수가 홀수
- +00+
    - 앞에 있는 펄스가 -
    - 대치 후 앞에 있는 1의 개수가 짝수
- 000+
    - 앞에 있는 펄수가 +
    - 대치 후 앞에 있는 1의 개수가 홀수
- -00-
    - 앞에 있는 펄스가 +
    - 대치 후 앞에 있는 1의 개수가 짝수

###### DC 성분

- 신호가 가지는 평균값
- 직류 성분을 없애는 것은 평균값을 0으로 만드는 것

- 비트 수가 늘어나지 않으므로 데이터 전송 속도에 손해가 없음

## 디지털 데이터 → 아날로그 신호

- 통신망
    - 전화망은 음성을 전송하기 적합
- 디지털 데이터는 음성이 가지는 대역폭(300~3400Hz)보다 더 높은 대역폭을 요구
- 따라서 디지털 데이터를 전송에 용이한 형태(음성 대역폭 안에 들어갈 수 있도록) 변경해야 함
⇒ Modulation
- 전송한 아날로그 신호를 다시 디지털 데이터로 변경하기 위해
⇒ Demodulation
- 3가지 방식
    - Amplitude shift keying(ASK) - 진폭
    - Frequency shift keying(FSK) - 주파수
    - Phase shift keyign(PSK) - 위상

#### Amplitude shift keying(ASK)

- 반송 주파수를 이용하여 0이냐 1이냐에 따라 다른 진폭을 갖는다.
- 사인파
- 진폭이 0 또는 1
- 신호가 급격하게 변화하므로 바람직하지 않음
- 비효율적
- 전화선에서 1200bps까지 가능 → 지금 사용 불가능, 매우 느림
- 광섬유를 사용하면 속도를 높일 수 있음

#### Binary Frequency shift keying(BFSK)

- 주파수를 달리한다.
- 이진 1일 때는 주파수가 f1
- 이진 0일 때는 주파수가 f2
- 두 개의 반송 주파수를 사용
- 두 개의 주파수가 반송 주파수 근처에 있음
- 에러에 덜 민감하므로 신뢰성이 높고 바람직함
- 전화선에서 1200bps까지 올릴 수 있음
- 더 높은 무선 주파수
- 동축 케이블을 사용하면 더 높은 주파수, 더 높은 전송속도를 제공할 수 있음

###### 전화선

- 음성 대역폭 300~3400Hz
- 디지털 신호를 전송할 때 양방향으로 전송(source-destination)하기 위해 대역폭을 반으로 나눔
    - 1700Hz 아래쪽 대역은 전송에 사용
    - 1700Hz 위쪽 대역은 수신에 사용
- upstream : 전화기에서 망쪽으로 가는 것
- downstream : 망에서 전화기 쪽으로 가는 것
- 각 방향에 대해 0,1이 있음
    - upstream에서 주파수가 1070Hz일 때 0, 1270Hz일 때 1
    - downstream에서 주파수가 2025Hz일 때 0, 2225Hz일 때 1

#### Multiple FSK(MFSK)

- 더 많은 주파수 성분 사용
- 하나의 주파수에 많은 비트 할당
- 대역폭을 효율적을 사용할 수 있음
- But 복잡도 증가, 에러가 일어날 확률이 높아짐

#### Phase shift keying(PSK)

- 위상에 따라 0,1을 구분
- 가장 기본적인 형태 : Binary PSK(BPSK)
    - 두 개의 위상 사용
- Differential PSK(DPSK)
    - 이전에 전송된 것과 상대적으로 천이가 일어남
    - 1이 시작할 때마다 위상의 천이가 일어남

#### 대역폭 효율

- ASK
    - $B_T = (1 + r)R$
    - R : 전송 속도(data rate)
    - r : 전송 대역폭(transmission bandwidth)
        - 기술에 의존적
    - $B_T$가 작을수록 효율적
    - Bandwidth Efficiency = $R/B_T$ → 클수록 좋음
        
        1/(1+r)
        
- FSK
    - 주파수 레벨 수를 증가시킬수록 대역폭 효율이 나빠짐
    - 에러 확률의 관점에서 좋음
    - MFSK : $B_T = ({(1+r)M\over log_2M})R$
- PSK
    - 위상 레벨 수를 증가시킬수록 대역폭의 효율이 좋아짐
    - 주파수 이용률 관점에서 좋음
    - MPSK : $B_T = ({1+r\over L})R = ({1+r\over log_2M})R$

#### Quadrature Amplitude Modulation(QAM)

###### Quadrature PSK(QPSK)

- 많이 사용
- 위상을 여려 개로 나눠서 사용하는 형태
- 위상을 4개 사용
- 한 위상에 대해 2비트 사용 00, 01, 10, 11
- 1비트보다 더 많은 것을 표현할 수 있으므로 더 효율적
- 위상은 360도이므로 4개로 나누면 90도
- 2비트로 매핑 가능
- 9600bps modem은 12개의 각도 사용 (30도씩) 진폭을 4개 사용
→ 총 개수 16
→ 4비트로 매핑