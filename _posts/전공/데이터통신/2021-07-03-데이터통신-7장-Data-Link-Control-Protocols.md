---
layout: single
title: "[데이터통신] 7장 Data Link Control Protocols"
excerpt: "7장 Data Link Control Protocols"
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

## Data Link Control Protocols

- 데이터를 전송하기 위해, control을 하기위해, 물리적 층 위에 논리적 층이 추가되어야한다.
    - L1 : physical layer
    - L2 : data link layer
        - point와 point간의 신뢰성있는 전송 보장
        - error control
        - flow control
    - L3 : network layer
        - routing
    - L4 : Transport layer
        - end와 end 사이 신뢰성있는 전송 보장
        - error control
    - L5 : session layer
    - L6 : presentation layer
    - L7 : application layer
- 하나의 링크를 통해 데이터의 교환을 다뤄야함
    - frame synchronization 프레임 동기화
        - 언제 프레임이 시작되고 끝나는지 알아야함
        - 수신측이 받을 수 있는 속도보다 더 빠르게 보내면 안됨
    - flow control 흐름 제어
    - error control
        - 에러를 감지하고 정정할 수 있어야함
    - addressing
        - 통신하는 대상이 여러개이므로 지칭할 수 있어야함
    - control and data
        - 수신측에서 control정보인지 data정보인지 구별할 수 있어야함
    - link management
        - 링크를 관리할 수 있어야 함

## Flow Control

- transmitting entity는 receiving entity가 받는 것보다 더 빠르게 전송하면 안됨
    - receiver는 버퍼가 존재
    - 버퍼의 크기가 한정됨
    - 버퍼링할 수 있는 능력보다 더 빠른 속도로 들어오면 버퍼가 넘침 → 오버플로우 발생 → 전송할 데이터 손실
    - 버퍼가 넘치는 것을 방지하기 위해 flow control필요
- 영향을 미치는 요소
    - 전송 시간 transmission time
        - 링크를 통해 프레임의 첫번째 비트가 나가는 시간부터 마지막 비트가 나갈때까지 시간
        - 프레임의 비트수가 많아질 수록 길어짐
        - data rate가 짧을수록 짧아짐
        - 프레임의 사이즈와 data rate에 따라 결정됨
    - 전파 시간
        - 첫번째 비트가 출발해서 도착할때까지의 시간
        - 거리에 따라 결정됨
- 에러가 없으면 모두 수신
    - 에러의 종류 : 손실, 올바르지 않는 데이터 수신

## Stop and Wait

- flow control의 가장 단순한 방식
- 데이터를 전송하고 전송할 데이터가 더 있더라도 수신측에서 잘 받았다는 acknowledge가 올때까지 기다림
1. source가 프레임을 전송
2. destination은 프레임을 받고 ACK로 응답
3. source는 ACK를 받기 전까지 다음 프레임을 보내지 않음
- 긴 메시지를 몇개만 보낼 때 적합
    - 실제로 긴 메시지를 보낼 때는 여러개의 블럭으로 잘라서 전송
    - 작은 블럭으로 잘라서 보낼때는 효율적이지 않음
    - 긴 프레임을 여러개의 블럭으로 나누는 이유
        - error control : 짧은 메시지가 성공적으로 전송될 확률이 높음
        - 효율성 : 에러가 일어났을 경우 긴 메시지는 재전송할 양이 많음
        - fairness 공평성 : 긴 메시지를 전송하면 끝날 때까지 다른 메시지를 전송할 수 없음

## Stop and Wait Link Utilization

- 프레임 길이(전송 시간) : 1
- t0 : 프레임 첫번째 비트가 출발한 시간
- a : 전파시간, 첫번째 비트가 receiver에 도착한 시간
- t0 + 1 : 프레잉의 마지막 비트가 출발한 시간
- t0 + 1 + a : 마지막 비트가 수신기에 도착
- t0 + 1 + 2a : ACK가 도착하는 시간
- 이용률 : 실제 데이터를 전송하는 시간
- 이용률이 클수록 좋음
    1. 프레임의 사이즈가 긴 경우
    2. 거리가 짧을 때
    3. data rate이 느릴 때(저속망에서 적합)
- 이용률 = t(frame) /( t(frame) + 2t(pmp)) = 1 / (1 + 2(t(pmp)/t(frame))) = 1/(1 + 2a)
    
    a = t(pmp)/t(frame)
    
- 이용률 증가시키려면 → frame길이를 길게, 저속망, propagation을 짧게, 거리를 짧게

## Sliding Windows Flow Control

- ACK를 받지 않더라도 다수개의 프레임을 전송할 수 있도록 하는 것
- ACK를 받지 않고 전송할 수 있는 프레임의 수를 제한
- sequence number field
    - 보낼 때마다 증가
    - window사이즈는 2^k -1
- 양방향 링크이면 piggyback ACK가 가능
    - 데이터를 보내면서 ACK도 함께 보냄
- ACK종류
    - Positive
        - Receive Ready(RR)
        - Receive Not Readay(RNR)
    - Negative
        - Reject
        - Selective Reject

## Error Control Techniques

- Error detection
- Positive acknowledgment
- Negative acknowledgment and retransmission
- Retransmission after timeout
- Lost frames
    - 프레임이 전송되지 않은 것
    - Time out
- Damaged frames
    - 에러 검출
    - 재전송 요청

## Automatic Repeat Request (ARQ)

- 에러가 있는 프레임을 받은 경우 어떻게 action할지
- 종류
    - stop and wait
    - go back N
    - selective reject

## Stop and Wait ARQ

- Source가 하나의 프레임을 전송
- ACK를 기다림
    - positive 또는 negative ACK를 받을 수 있음
    - 또는 time out되어 재전송할 수 있음
- ACK가 중간에 없어진 경우
    - 송신측에서 time out이 되고 재전송
    - 수신측에서 똑같은 것을 2개 받음
    - 이것을 방지할 방법이 필요
    - ACK0과 ACK1 번갈아 사용
- 장점 : 단순
- 단점 : 비효율적

## Go-Back-N ARQ

## Selective-Reject(ARQ)

## High Level Data Link Control (HDLC)

- 가장 중요한 data link control protocol
- Station types
    - Primary : 주
    - Secondary : 종
    - Combined : pc와 pc 대등한 관계
- Link configuration 링크 구성 방법
    - Unbalanced : primary와 secondary 간의 통신
    - Balanced : 대등한 관계 combined station

## HDLC Data Transfer Modes 전송 모드

#### Normal Response Mode(NRM)

- primary와 secondary간의 전송 모드
- unbalanced configuration
- primary가  전송을 시작

#### Asynchronous Balanced Mode(ABM)

- 두 개의 스테이션 중 언제 전송을 시작할지 알 수 없음
- balanced configuration
- polling이 필요 없음

#### Asynchronous Response Mode(ARM)

- unbalanced configuration
- secondary도 primary의 허락없이 전송할 수 있음

## HDLC Frame Structure

- Flag : 8bit
- Address  : 8bit, 8비트 단위로 확장 가능
- Control : 8 or 16비트
- Information : 가변적
- FCS : 16 or 32 비트
- Flag

## Flag Fields and Bit Stuffing

- flag로 시작해서 flag로 끝남
- 01111110
- flag가 아닌데 flag와 같은 패턴이 올 수 있음
- 0을 삽입하여 방지
- flag가 아닌 다른 필드에서 1이 5번 나오면 0을 삽입하여 전송 : bit stuffing
- 수신측에서는 1이 다섯개나오고 0이 나오면 0제거

## Address Field

- 8비트
- 확장 가능
- 첫번째 비트가 0이면 Address Field가 계속됨
- 1이면 끝남
- 11111111이면 broadcast

## Control Field

- 프레임의 타입
    - Information
        - 0 N(S) P/F N(R)
        - piggyback
    - Supervisory
        - 1 0 S P/F N(R)
    - Unnumbered
        - 1 1 M P/F M
- Polling 1 : 응답요청
- Final 0 : 응답
- 16비트
    - 7비트 sequence number사용할 때

## Information and Frame Check Sequence(FCS) Fields

FCS : 에러 체크

## HDLC Operation