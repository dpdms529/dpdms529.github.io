---
layout: single
title: "[데이터통신] 6장 Error Detection and Correction"
excerpt: "6장 Error Detection and Correction"
date: 2021-07-03T00:00:00+09:00
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

## Asynchronous and Synchronous Transmission

- 전송방식에는 비동기 방식과 동기 방식이 있음
- transmitter와 receiver사이의 타이밍을 맞춰야 함
- 데이터 전송이 언제 시작되고 끝나는지, 데이터 내에서 각각의 비트를 구분할 수 있어야 함
- receiver는 각 간격의 중간을 샘플링
- transmitter의 clock speed와 receiver의 clock speed가 달라서 오차가 생길 수 있음
    - 0이 계속 될 때 또는 1일 계속 될 때 문제 발생
- clock을 동기화 시킴으로써 해결
    - transmitter와 receiver가 같은 clock사용
        - 별도의 라인 사용
            - 비용이 큼 → 잘 사용하지 않음
        - 인코딩
            - Manchester
                - 매 비트마다 천이가 일어나서 동기 일어남
                - 더 큰 대역폭 요구 → 고속망에 적합하지 않음
        - Asynchronous transmission
            - 동기가 한번 일어남(시작할 때)
            - 긴 데이터를 보낼 수 없음 → 오차가 누적됨
            - 제한된 수만 가능
        - Synchronous transmission
            - 인코딩 방식 사용
            - Manchester
            - 큰 블럭을 전송할 수 있음

## Asynchronous Transmission

- 데이터 전송 중에 재동기 일어나지 않음
→ 긴 데이터를 보낼 수 없음
    - 8비트 이내 (한 Character)
    - receiver는 각 character마다 동기화할 수 있는 기회는 갖지만 캐릭터 내에서는 동기화할 수 없음
- 단순 & 쌈
    - 오버헤드가 크다 (20%정도)
- 블럭이 커질수록 에러가 커짐 ← 오차가 누적되므로
- 키보드같은데 적합
    - 800bps → 느림

- 데이터를 전송하지 않을 때 5V
- 전송할 데이터가 있을 때 0V → start bit
- 패리티 비트 : 에러를 검출하기 위해 사용
- 전송이 끝났을 때 1 → stop bit
    - 길이가 1, 2, 1.5비트일 수 있음
- 오버헤드가 큼
    - 8비트를 전송하기 위해 3~4비트가 붙음
    - 링크의 이용률이 높지 않음

## Synchronous Transmission

- 블럭을 전송
    - start bit와 stop비트가 없음
    - flag사용
        - 미리 정의된 유니크한 비트 패턴
- clock은 동기화 해야함
    - 별도의 clock라인 사용
    - 데이터에 clock신호를 실어서 보냄
- 데이터의 시작과 끝을 나타낼 수 있어야 함 → flag사용
- 동기화를 맞추기 위해 0,1반복
- 데이터를 전송하지 않을 때는 그런 패턴 전송
- 데이터 블럭의 길이가 길어질 수록 오버헤드가 작아짐

## Types of Errors

- 에러 : 데이터를 전송했을 때 데이터의 변경이 이루어진 것
    - 1을 전송했는데 0을 받음
    - 0을 전송했는데 1을 받음

#### single bit errors

- random error
- 가끔가다 한 비트씩 에러가 일어남
- 에러를 검출하기도 쉽고 정정하기도 쉬움
    - 패리티 비트 사용 가능
        - 패리티 검사는 2비트의 에러가 일어나면 검출이 안됨
        - 짝수비트의 에러는 검출되지 않음
- white noise가 주원인

#### burst errors

- 군집성 에러
- 에러가 연속해서 여러개가 동시에 변함
- 통신망에서는 burst error가 많이 일어남
- 패리티 검사 사용할 수 없음
- 무선망에서 impulse noise나 fading이 원인
- 고속에서 영향이 크다

## Error Detection

- 에러를 검출할 수 있어야함
- Pb : bit error rate(비트의 오류 확률)
- P1 : 프레임을 받았을 때 프레임에 에러없이 도착할 확률
    - 프레임 : 비트의 모임
    - P1 = (1-Pb)^8
- P2 : 프레임이 도착했을 때 하나 또는 그 이상의 에러가 있었는데 감지되지 않고 도착하는 확률
    - 에러를 검출하지 못하므로 문제 발생
- P3 : 에러 감지 알고리즘이 사용되는데 어떤 프레임이 에러를 가지고 도착했는데 에러가 모두 감지되어 도착하는 확률
- 프레임의 길이가 짧을수록 성공적으로 도착할 확률이 높음
- 프레임을 너무 작게 전송하면 오버헤드가 큼
- 적절한 사이즈 필요

#### Error Detection Process

###### Transmitter

- 보낼 데이터 k bit
- k bit 사용해서 operation F 사용 E = f(data)
- f함수의 변수 data
- data를 이용해서 코드 생성
- 코드를 data에 붙여서 보냄
- 전송되는 비트의 총 수는 n bits
- 에러 감지를 위해 추가된 비트 수는 n-k bits

###### Receiver

- n bit 수신
- k bit에 대해서 똑같은 함수 수행
- E' = f(data')
- E = E'이면 에러 없음

## Parity Check

- 가장 단순한 에러를 감지하는 방식
- 데이터 블록 끝에 패리티비트를 추가
- Even parity : 보낼 때 1의 개수를 짝수로
- Odd parity : 보낼 때 1의 개수를 홀수로
- 짝수개의 비트가 에러로 인해 invert되면 에러가 감지될 수 없다.

## The Internet Checksum

- 에러 정정능력이 패리티보다 좋음
- IP, TCP, UDP를 포함해서 많은 Internet standard protocol에 많이 사용됨
- Ones-complement operation 사용 (1의 보수)
    - 각각의 비트를 반대로 바꾸는 것
    - 0은 1로 1은 0으로
- 두 수를 더하면 캐리 발생할 수 있음
- 캐리 발생하면 맨 뒤에 1을 더함

#### Sender

덧셈해서 나온 값을 1의 보수로 만들어줌

#### Receiver

덧셈해서 나온 값이랑 sender가 보낸 값 더했을 때 모든 값이 1이 되면 에러 없음

## Cyclic Redundancy Check(CRC)

- k비트를 전송하기 위해 n-k비트의 frame check sequence(FCS)를 딸려서 보냄
- Transmitter와 Receiver가 데이터를 주고받기 위해 초기화를 함
    - P : polynomials
    - 보내고자하는 데이터 X
        - X/P = Q...R
        - 원래 보내고자하는 데이터에 나머지를 딸려 보냄
    - 수신측에 X + R 수신(원래 데이터 + 나머지)
    - X + R / P = Q...0
    - 나머지가 항상 0 → 에러 없음
    - P가 길수록 에러 감지능력이 좋음
    - 에러가 나더라도 P로 나눠 떨어질 수 있지만 P가 길수록 그 확률이 작음
    
#### Modulo 2 operation

- 0,1만 존재
- 올림수,내림수가 없음
- XOR
    - 같으면 0 다르면 1
    - 1의 개수가 짝수면 0 홀수면 1

#### Polynomials

P(x) = ... + d3*x^3 +d2* x^2 + d1*x^1 +d0* x^0

- modulo 2 연산 수행

T : 보내는 프레임 nbits

D : 전송하고자하는 데이터 kbits

F : FCS n-kbits

P : n-k+1

T = 2^(n-k) *D + R = Q + R/P + R/P = Q + (R+R)/P (R+R = 0)

2^(n-k)*D/P = Q…R = Q + R/P

XOR와 레지스터만 있으면 구현 가능
    

## Forward Error Correction

- Correction에는 Forward Error Correction(FEC)과 Backward Error  Correction(BEC)이 있음
- Backward Error Correction은 재전송 방식을 이용
- 재전송 방식이 무선통신에는 적합하지 않음
    - 무선은 유선에 비해 신뢰성이 낮음 ⇒ 에러 확률이 높음 ⇒ Pb가 높음
    - 재전송 요청이 많아짐
    - 전파지연이 긴 경우 재전송 요청하고 다시 받는데 오래 걸림
        - ex) 위성 통신
    - forward error correction방식 필요
- 에러를 발견한 수신측에서 정정
- 에러를 정정할 수 있는 코드를 포함해야함 → 데이터를 전송할 때 더 많은 데이터를 포함해서 전송해야 함
- 단거리 전송(LAN)은 재전송 방식 사용이 일반적

#### Codeword

- 내가 전송할 비트가 k비트이면 n비트에 매핑시킴
- n이 k보다 큼
- 101전송하고자 함 → 111 000 111
- k = 1 n = 3 → 오버헤드가 큼
- 정육면체
    - 인접한 점은 1비트만 다름
    - 정반대에는 반대 비트로 구성
    - 이웃은 한비트 에러
    - 이웃 안 겹침

#### Error Correction Process

###### Transmitter

데이터 kbits

FEC 인코더 → codeword생성하여 전송

###### Receiver

codeword 수신

FEC 디코더 → 원래 데이터

두비트 에러 나면 정정이 안됨 → 없애버림

## Block Code Principles

#### Hamming distance

- d(v1,v2)
- 두 개의 codeword에서 다른 비트의 수
- XOR사용해서 1의 개수 셈
- 5비트를 만들면 2비트 에러도 정정 가능

#### Redundancy of the code

- (n-k)/k = 오버헤드 / 원래 전송하고자 하는 데이터
- 작을수록 좋음

#### Code rate

- k / n = 원래 데이터 길이 / 전체 전송하는 비트의 수
- 클수록 좋음