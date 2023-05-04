---
layout: single
title: "[데이터통신] 8장 Multiplexing"
excerpt: "8장 Multiplexing"
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

## Multiplexing 다중화

- 하나의 물리적 라인이 다수개의 링크를 제공
- 여러개의 source and destination 쌍이 하나의 물리적 링크를 공유
- 물리적 링크의 용량이 충분히 크고 이것을 n개의 source and destination에 공유
- FDM, TDM, STDM

## Frequency Division multiplexing

- 주파수 대역을 나눈 것
- sub carrier frequency 서브 반송 주파수
- 시간축
- 시간을 연속적으로 사용
- transmitter에서 input이 subcarrier에 의해 modulation한 후 합함
    - 사용되는 주파수가 다르므로 영향을 미치지 않음
- receiver에서 bandpass filter를 사용하여 측정한 대역만 출력한 후 반송주파수 사용하여 각각 디모듈레이션

## Analog Carrier Systems

- AT&T : 미국
- ITU-T : 국제
- Group : 12개의 음성 채널 48kHz, 60~108kHz
- Supergroup : 5개의 그룹, 60개의 음성채널, 240kHz, 312~552kHz
- Mastergroup : 10개의 슈퍼그룹, 600개의 음성채널, 2400kHz
    - ITU-T는 5개의 슈퍼 그룹

## WDM 파장분할다중화

- 주파수가 다른 여러 개의 광선
- 광섬유를 통해 다수개의 파장 전송
    - 160개로 파장 나눌 수 있음
    - 전송 속도 10Gbps
- 하나의 광섬유가 가지는 용량이 매우 큼
    - 수십 Tbps = 10^13bps
- 이용률을 높이기 위해 멀티플렉싱
- 1600Gps
- DWDM(Dense wavelength division multiplexing)
    - 파장을 조밀하게 나누는 것
    - 1나노미터로 나눔

## TDM(Time Division Multiplexing)

- 정해진 시간마다 순서가 할당됨
- 동기화
- Transmitter
    - 버퍼를 이용(메모리)
    - 디지털 데이터가 들어오면 버퍼에 넣음
    - scan operation을 통해 전송
- time slot : 각각의 할당되는 시간
- frame : slot이 모여 하나의 주기가 된 것
- Receiver

## TDM Link Control

- 헤더와 트레일러가 필요 없음
- data link control protocols이 필요 없음

## Frame

- 동기 맞추기 위해 프레임 앞에 동기 신호가 있음
- 101010

## Pulse Stuffing

- 배수관계를 맞추기 위해 의미 없는 비트 삽입

## DS-1 Transmission Format

- 동기 비트 1개
- 각각의 타임 슬롯 크기 : 8bit
- 타임 슬롯 개수 : 24
- Frame : 24*8 + 1 = 193bits
- 1초에 8000번 하나의 프레임이 나옴
- 193bits/frame * 8000frame/sec = 193*8000 bit/sec = 1.544Mbps (data rate)
- 1/8000 = 125μsec

## SONET/SDH

- Synchronous Optical Network(ANSI)
- Synchronous Digital Heirarchy(ITU-T)
- Optical carrier level 1 (OC-1) 51.84Mbps
    - (90*8*9)bit/Frame * 8000Frame/sec = 9**8**9*8000 bit/sec = 51.84Mbps

## Statistical TDM

- A만 전송할 것이 있거나 B만 전송할 것이 있을 경우 문제 -> 통계적 TDM
- 타임슬롯의 주인이 없음
- 요구에 의해서 할당
- A가 전송할 데이터가 많으면 A에게 더 많이 할당
- 타임 슬롯의 주인이 시시각각 달라짐
    - 전송할 때 주소가 필요
- 오버헤드(주소 표시)가 있지만 채널을 더 효율적으로 사용 가능
    - 오버헤드 줄이는 방법
        - 상대 주소 사용
        - 가변길이코딩
- 사이즈가 일정할 때는 길이 정보 필요 없음
- 길이가 가변일 때는 길이 정보 필요

## Single-server queues with constant service times and poisson (random)arrivals

- λ(도착률) -> buffer queue -> server -> μ(service rate)
- λ : 프로세스가 도착할 확률
- μ : 프로세스가 서비스를 끝내고 나가는 비율
- ρ : load 부하, 0에서 1사이 값 λ/μ = λ*Ts          1/μ = Ts(service time)
- 통신에서 서버는 채널
- 통신망에서 손님은 frame
- 서버의 이용률
- 서버에 머무르는 customer의 수 -> 많으면 기다리는 시간 길어짐

## Cable Modems

#### Downstream

#### Upstream

## Cable spectrum division

- User to network data(upstream) : 5~40MHz
- Television delivery(downstream) : 50~550MHz
- Network to user data(downstream) : 550~750MHz

## Asymmetrical Digital Subscriber line(ADSL)

- Access network : 전화기에서 교환기까지 subscriber line
- 전화선은 tp
- TP를 대상으로 만들어짐
- 비대칭 : downstream과 upstream에 대한 bandwidth가 다름
- Tp의 용량이 충분하지 않으므로 효율적으로 사용하기 위해
- Download가 많음
- Downstream은 크게 upstream은 작게
- Subscriber(전화기)와 network(교환기) 사이의 링크
- Tp를 위한 것
- Downstream이 더 큼
- Frequency Division Multiplexing을 사용
- 기존의 tp는 전화를 위한 것
- 기존 음성 서비스(POTS)에 영향을 미치지 않으면서 데이터 전송해야 함
- 낮은 대역에는 손을 대지 않음 데이터 서비스는 25kHz이상의 대역 사용
    - 이렇게 하기 위해 Echo cancellation, FDM사용 
- 거리는 최대 5.5km
- 거리가 멀어질수록 전송속도는 낮아짐
- 거리가 멀수록 노이즈가 많음
- 전송의 퀄리티 낮아짐 -> 에러률 높아짐
- 에러를 줄이기 위해서는 한 비트 에너지를 크게 가져야 함 -> 한 비트 폭을 크게 가져야 함
    - FDM
        - 주파수 대역을 분할
        - 대역이 고정되어 있음
    - Echo cancellation
        - 에코를 제거
        - 가변적
        
        ![image](https://user-images.githubusercontent.com/60471550/235668207-d8d593fd-0a0c-403f-9ae5-dd2a5ad38240.png)
        
        - 장점 : 융통성이 있다.
        - 단점 : 받고 싶지 않은 데이터도 받을 수 있음 -> 제거해야 함
    
## DMT(Discrete Multitone)

- 전체대역을 작은 서브대역으로 나눈 것
- 각각의 주파수 대역에 대한 gain이 다 다름
- 신호 퀄리티와 gain이 관련 있음
- 서브 밴드의 품질이 좋은 데는 많은 비트 전송
- 품질 나쁜데는 적은 비트 전송 (에러비율이 많으므로 속도를 줄임)
- Gain이 클수록 좋음 -> 전송 능력이 좋음
- 서브채널은 4kHz
- 각각의 서브채널을 측정해보면 SNR이 다름
- Signal to noise rate 클수록 좋음
- 이론적으로 15Mbps 실제로는 1.5~9Mbps

## xDSL

- ADSL
    - Asymmetric
    - DMT
- HDSL
    - Symmetric
- SDSL
    - Symmetric
- VDSL
    - Asymmetric
- 서비스하는 거리에 차이가 큼

## FDMA

- Frequency-Division Multiple Access 하나의 기지국에 다수개의 station에 서비스
- station마다 다른 주파수를 할당 받아서 접근
- 여러 개의 station이 스펙트럼을 공유하는 기술
- Base station이 주파수 할당
- 각각의 station은 다른 주파수 대역을 사용한다.
- 서브 채널이 사용되지 않으면 용량 낭비
- 서브채널과 서브채널 사이에 서로의 간섭을 피하기 위해 guard band가 필요
- 주파수를 나눠서 쓰기 때문에 오버헤드가 상대적으로 작음

## TDMA

- Time-division Multiple Access
- 시간을 각각의 station에 할당
- 시간이 주기적으로 돌아옴
- 하나하나의 slot이 하나의 유적에게 할당
- 그 slot이 주기적으로 할당 => 채널
- 한 주기에 해당하는 slot의 모임을 frame
- 하나의 frame은 다수개의 slot으로 구성
- 각각의 slot은 사용자가 다름
- Logical subchannel : 시간들의 모임
- 각각의 서브채널이 station에 할당
- 각각의 station에 대해서 데이터 전송은 연속적이지 않고 burst단위로 일어남
- Guard time필요 정확한 동기가 맞지 않으므로
- Downlink 채널은 경우에 따라 분리된 주파수 대역 사용
- Uplink downlink가 같은 주파수 대역을 사용할 수 있음