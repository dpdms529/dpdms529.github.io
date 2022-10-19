---
layout: single
title: "[인공지능] 3장 Solving Problems by Searching"
excerpt: "3장 Solving Problems by Searching"
date: 2022-10-19T17:55:00+09:00
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

## 문제 유형

- Single-state problem
    - 상태가 결정적이고, 전체 관찰 가능
- Conformant problem
    - 관찰 불가능
- Contigency problem
    - 상태가 결정적이지 않고, 부분적으로 관찰 가능
- Exploration problem
    - 알 수 없는 상태 공간

## Single-state problem 공식화

- 문제 정의
    - 상태(상태 공간)
    - 다음수 함수(전이 모델)
    - 시작 상태
    - 목표 상태
- 솔루션 : 시작 상태에서 목표 상태까지의 행동들의 순서
- 탐색 : 솔루션을 찾기 위한 과정
    - 입력 : 문제
    - 출력 : 솔루션

## 추상화

- 현실 세계는 복잡
- 문제를 해결하기 위해서는 추상화 필요
- 추상화 된 문제는 원래의 문제보다 단순해야 함

## 솔루션 탐색

- 탐색 트리
    - 루트 노드는 시작 상태
    - 자식 노드는 다음 상태
    - 노드는 상태를 포함
    - 간선에는 행동과 비용이 표시됨

```basic
function TREE-SEARCH(problem, strategy) return solution, or failure
		문제의 처음 상태로 탐색 트리 초기화
		loop do
				if 확장할 후보가 없음 then return failure
				strategy에 따라 확장할 리프 노드 선택
				if 노드가 목표 상태 포함 then return solution
				else 노드 확장 후 탐색 트리에 결과 노드 추가
```

## 상태 vs 노드

- 상태 : 물리적 구성
- 노드 : 부모, 자식, 깊이, 비용 정보를 가지는 자료구조
- 서로 다른 노드가 같은 상태를 가질 수 있음

## 탐색 기준

- 완전성 : 솔루션이 존재한다면 항상 솔루션을 찾아내는가?
- 최적성 : 항상 최소 비용의 솔루션을 찾아내는가?
- 시간 복잡도 : 생성되는 노드의 수
- 공간 복잡도 : 메모리의 최대 노드 수
- 시간 복잡도와 공간 복잡도 측정
    - n : 문제에서 상태의 수
    - b : 탐색 트리의 최대 브랜치 수
    - d : 최소 비용 솔루션의 깊이
    - m : 탐색 트리의 최대 깊이

## 탐색 전략

- 전략 : 노드 확장 순서를 선택하는 것
- Uninformed strategies(맹목적 탐색)
    - Depth-first search
    - Breadth-first search
    - Depth-limited search
    - Uniform-cost searcg
    - Iterative deepening search
- Informed(Heuristic) strategies(정보이용 탐색)
    - Best First / Greedy Search
    - A*

## BFS(너비 우선 탐색)

- 가장 깊이가 얕고 확장되지 않은 노드부터 탐색
- 완전성 : O
- 최적성 : 각 경로의 비용이 동일하면 O
- 시간복잡도 : $O(b^d)$
- 공간복잡도 : $O(b^d)$
    - 공간복잡도가 너무 큼

## DFS(깊이 우선 탐색)

- 깊이가 깊은 노드부터 탐색
- 완전성 : 깊이가 유한하면 O, 무한하면 X
- 최적성 : X
- 시간복잡도 : $O(b^m)$
- 공간복잡도 : $O(bm)$

## Depth-limited search

- 깊이가 제한된 DFS
- 완전성 : X
- 최적성 : X
- 시간복잡도 : $O(b^L)$
- 공간복잡도 : $O(bL)$

## Iterative deepening search(반복적 깊이심화 탐색)

- DFS를 반복
    1. 처음에는 깊이 제한을 1로 해서 DFS 진행
    2. 탐색에 실패하면 깊이 제한을 +1해서 DFS진행
    3. 탐색에 성공할 때까지 2번 반복
- 완전성 : O
- 최적성 : 각 경로의 비용이 모두 1일 때 O
- 시간복잡도 : $O(b^d)$
- 공간복잡도 : $O(bd)$

## Uniform-cost search

- BFS는 이동 횟수를 적은 경로를 찾기 때문에 최소 비용 경로를 찾지는 않음
- 우선순위 큐 사용하여 비용이 작은 노드 먼저 탐색
- 목표 상태를 우선순위 큐에서 꺼내면 탐색 멈춤
- 각 노드에 비용 함수 적용

```basic
우선순위큐에 처음 상태 추가
while 큐가 비어있지 않음
		Node = head(queue)
		if Node가 목표 상태 then return Node
		Node의 자식 노드들 우선순위큐에 추가
```

- 완전성 : O
- 최적성 : O
- 시간복잡도 : $O(b^{C^*/\epsilon})$
- 공간복잡도 : $O(b^{C^*/\epsilon})$
- 장점 : 완전하고 최적임
- 단점 : 목표 방향이 아닌 방향도 모두 탐색 → 비효율적

## Best-first search

- 각 노드에 평가 함수 사용
    - 바람직한 정도를 측정
- 가장 바람직하고 확장되지 않은 노드부터 탐색

## Greedy search

- 목표와 가까운 노드부터 탐색
- 평가 함수 h(n)
    - heuristic : 최적은 아니지만 골을 찾기에 충분한 실용적인 방법
- 각 상태에 대해 목표에 가장 근접한 비용 추정치
- 완전성 : X
- 최적성 : X
- 시간복잡도 : $O(b^m)$
- 공간복잡도 : $O(b^m)$

## A* search

- 이미 지나온 경로 중 비싼 곳은 가지 않음
- Uniform-cost search와 Greedy search를 결합한 것
- 평가 함수 f(n) = g(n) + h(n)
    - g(n)  : n까지 가는데 드는 비용
    - h(n) : n에서 목표까지 가는데 예상되는 비용
- 목표 상태를 가지는 노드를 큐에서 꺼냈을 탐색 멈춤
- 완전성 : O
- 최적성 : O
- 휴리스틱 함수를 잘 정의해야 함

## 휴리스틱 허용성

- h(n) ≤ h*(n)일 때 허용 가능(최적)
- h*(n) : n에서 목표까지의 실제 비용

## A*의 최적도

- 가정
    - $G_1$ : 최적의 목표
    - $G_2$ : $G_1$ 다음 최적의 목표
    - h : 최적의 휴리스틱
- 명제
    - $G_1$이 $G_2$보다 먼저 큐에서 나올 것이다.
- 증명
    
    n은 $G_1$까지 가는 경로에 존재하는 노드
    
    $f(G_2) = g(G_2) > g(G_1) \ge f(n)$
    
    $f(G_2) > f(n)$이므로 A*는 $G_2$를 선택하지 않을 것이다.
    

## Uniform Cost Search vs A*

- Uniform Cost Search는 모든 방향으로 확장하며 탐색
- A*는 목표 방향으로 확장하며 탐색