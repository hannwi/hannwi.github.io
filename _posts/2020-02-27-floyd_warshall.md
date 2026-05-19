---
layout: post
title:  "Floyd-Warshall Algorithm 01 (Intro)"
crawlertitle: "Floyd-Warshall Algorithm 01 (Intro)"
summary: "Study Floyd-Warshall algorithm"
date:   2020-02-27
categories: posts
tags: 'Floyd-Warshall'
---

### 모든 노드 쌍의 최단거리 구하기
각 노드마다 Dijkstra 수행? (총 N 번)

### 경유점
그래프의 경로(path)에서 시작점, 끝점을 제외한 노드

### 경유점을 이용한 최단경로 정의
경유점 집합 S를 포함한 u -> v 최단경로 Ds(u,v)
구하고자 하는 최단경로: 전체 정점 집합 V를 경유점으로 하는 최단경로 Dv(u,v)

### 경유점 개념을 이용한 Dynamic Programming
#### 문제를 sub-problem 으로 쪼개기 (Top-down)
u에서 v까지의 최단거리는 아래와 같은 두 경우로 분리된다.
D(u,v)가 정점 x를 경유하지 않는 case
Dv-{x}(u,v)
정점 x를 경유하는 case
Dv-{x}(u,x) + Dv-{x}(x,v)
점화식은 아래와 같이 정의된다.
Ds(u,v)=min(Ds-{x}(u,v), Ds-{x}(u,x)+Ds-{x}(x,v))

#### Iteration 예시 (Bottom-up)
노드의 갯수가 총 N 개일 때, 1번부터 N번까지 차례대로 경유 노드를 추가해나간다.
1st iteration (모든 u,v 쌍에 대해 계산)
D{1}(u,v)=min(D{none}(u,v), D{none}(u,1)+D{none}(1,v))
직접 연결된 간선의 가중치 값이 곧 아무것도 경유하지 않는 최단거리가 된다.
2nd iteration (모든 u,v 쌍에 대해 계산)
D{1,2}(u,v)=min(D{1}(u,v), D{1}(u,2)+D{1}(2,v))
경유점을 추가하는 순서?
아무렇게나 추가해도 상관없으므로, 구현 편의상 노드의 번호 순서대로 추가한다. 단, 문제의 종류에 따라 별도의 특정 순서대로 경유점을 추가해야하는 경우도 있으므로 유의할 것.

#### Pseudo Code
for(k=1:V)
	for(u=1:V)
		for(v=1:V)
			C[k][u][v] = min(C[k-1][u][v], C[k-1][u][k]+C[k-1][k][v])
왜 경유점을 가장 바깥 for 문에 위치하는지?
위의 식에서 볼 수 있듯이, 새로운 경유점을 포함한 최단거리를 구하려면 그 경유점이 시작점/끝점일 때의 최단거리가 이미 계산되어있어야 한다. 따라서 순서상 모든 노드 쌍의 최단 거리를 먼저 구한 뒤에 새로운 경유점을 추가해야한다.

### Dijkstra vs. Floyd
Dijkstra
정해진 시작노드로부터의 각 노드까지의 최단거리를 구함
Greedy search 로 최단 노드
간선 개수만큼 탐색

Floyd
모든 노드쌍의 최단거리를 구함
Dynamic programming 으로 최단거리를 갱신
	경유점의 개념을 이용하여 문제를 sub-problem 으로 분할
노드 개수의 세제곱만큼 탐색

### 관련 문제
음주 운전 단속
https://algospot.com/judge/problem/read/DRUNKEN
선거 공약
https://algospot.com/judge/problem/read/PROMISES

