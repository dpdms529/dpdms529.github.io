---
layout: single
title: "[인공지능] 2장 Intelligent Agents"
excerpt: "2장 Intelligent Agents"
date: 2022-10-19T17:14:00+09:00
toc: true
toc_sticky: true
use_math: true
categories:
  - CS 
  - AI
tags:
  - CS
  - AI
---

## 에이전트(Agent)

- 인식하고 행동하는 개체
    - 사람, 로봇 등
- 센서와 작동기를 통해 환경과 상호작용
- 어떤 주어진 순간에 에이전트가 선택한 행동은 인식된 데이터따라 결정됨
- 인식된 시퀀스 정보로부터 행동을 도출하는 함수
    - $f : \Rho^* \rightarrow \Alpha$

![Untitled](https://user-images.githubusercontent.com/60471550/196634835-0df65bdf-04b2-4cf5-8666-c5f260581449.png)

## 합리적인 에이전트의 정의

- 합리적인 에이전트는 인식할 수 있는 각 시퀀스 정보에 대해 최대의 성능을 도출할 것으로 예상되는 행동을 선택해야 함
- 인식된 정보로부터 얻을 수 있는 정보와 이미 알고 있는 정보를 활용
- 합리적 : 예상되는 효용치를 최대화
- 예) 팩맨
    - 성능 측정 기준 : 점수 → 가장 많은 점수를 받도록 해야 함
    - 인식된 정보 : 유령의 움직임, 팩맨의 위치 등
    - 이미 알고 있는 정보 : 파워 알맹이를 먹으면 팩맨이 유령을 먹을 수 있음

## 작업 환경

- 합리적인 에이전트를 만들기 위해서는 작업 환경을 명시해야 함
    - 성능 측정 기준, 환경, 작동기, 센서
- 예) 팩맨
    - 성능 측정 기준 : 점수
    - 환경 : 미로, 유령 등
    - 작동기 : 이동 신호, 키보드를 누르는 장치
    - 센서 : 이미지 인식기, 카메라

## 환경 유형

| 관찰 범위 | 에이전트 개수 | 상태의 결정성 | 상태의 연속성/관련성 | 환경의 변화 | 상태의 개수 |
| --- | --- | --- | --- | --- | --- |
| 전체 | 1개 | 결정적, 현재 상태와 행동에 의해 다음 상태 정의 가능 | 단편적, 각 상태 간 관련 X | 없음(정적) | 유한 |
| 부분적 | 여러개 | 결정적 X, 다음 상태 알 수 없음 | 연속적, 각 상태 간 관련 O | 있음(동적) | 무한 |
- 현실 세계는 부분적으로 관찰 가능하며, 다음 상태를 알 수 없으며, 각 상태가 연속적이며, 환경이 동적으로 변하고, 상태가 무한하며 여러개의 에이전트가 존재함

## 에이전트 유형

### 단순 반영 에이전트(Simple reflex agents)

- 현재 인식된 정보를 기반으로 행동을 선택
- 이전 정보나 미래 상황을 고려하지 않음
- 현재 상황에서 좋은 것 선택

![Untitled 1](https://user-images.githubusercontent.com/60471550/196634966-f3420afe-cc91-4519-ac40-340e5d6730fa.png)


### 모델 기반 반영 에이전트(Model-based reflex agents)

- 내부의 히스토리 정보를 가지고 다음 상태 예측하여 행동 결정

![Untitled 2](https://user-images.githubusercontent.com/60471550/196635056-1fb46cca-4a72-40d0-8aca-f701a0938b74.png)

### 목표 기반 에이전트(Goal-based agents)

- 목표를 달성 가능한지 판단
- 목표 정보를 가져야 함

![Untitled 3](https://user-images.githubusercontent.com/60471550/196635145-f767e364-43a7-40ee-a00c-31da68f04c2a.png)

### 효용성 기반 에이전트(Utility-based agents)

- 목표 자체로는 높은 성능을 내는 행동을 하도록 하기에 부족
- 효용 함수(utility function)
    - 내부적인 성능 평가

![Untitled 4](https://user-images.githubusercontent.com/60471550/196635241-171c4a38-47a5-4e92-b438-052aceca9227.png)