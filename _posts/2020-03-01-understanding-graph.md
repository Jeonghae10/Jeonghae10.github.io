---
title: "[자료구조] 그래프(Graph)의 이해"
date: 2020-03-01 11:00:00 +0800
categories: [Algorithm, Data_Structure]
tags: [data_structure, graph, 자료구조, 그래프]
---
## 목표
> * 그래프(Graph)에 대해 설명할 수 있다.
> * 그래프(Graph) 관련 용어에 대해 설명할 수 있다.
> * 그래프(Graph)와 트리(tree)의 차이를 설명할 수 있다.

----------------------------------------------------
### 1. 그래프(Graph) 란 ?

* 실제 세계의 현상이나 사물을 정점(Vertex) 또는 노드(Node) 와 간선(Edge)로 표현한 자료구조   
![graph]({{"/assets/img/algorithm/graph/basic_graph.png" | relative_url}}){:height="300" width="400"}

### 2. 그래프(Graph) 관련 용어

* 노드(Node) : 위치를 의미. 정점(Vertex)라고도 함
* 간선(Edge) : 위치 간의 관계를 표시한 선(노드와 노드를 연결한 선). link or branch라고도 함.
* 인접 정점(adjacent Vertex) : 간선으로 직접 연결된 정점(또는 노드)
* 정점의 차수(Degree) : 무방향 그래프에서 하나의 정점에 인접한 정점의 수
  - 무방향 그래프에 존재하는 모든 정점의 차수의 합 = 그래프 간선의 갯수 * 2
* 진입 차수(in-Degree) : 방향 그래프에서 외부에서 오는 간선의 수
* 진출 차수(out-Degree) : 방향 그래프에서 외부로 향사는 간선의 수
* 경로 길이(Path Length) : 경로를 구성하기 위해 사용된 간선의 수
* 단순 경로(Simple Path): 시작 정점과 끝 정점을 제외하고 중복된 정점이 없는 경로
* 사이클(Cycle) : 단순 경로의 시작 정점과 끝 정점이 동일한 경우

### 3. 그래프(Graph)의 종료

* 무방향 그래프 vs 방향 그래프
  - 무방향 그래프(Undirected Graph)
    + 방향이 없는 그래프
    + 간선을 통해 각 노드에서 양방향으로 이동할 수 있음
    + 노드 A,B가 연결되어ㅓ 있을 경우 (A,B) 또는 (B,A)로 표기  

  ![undirected_graph]({{"/assets/img/algorithm/graph/undirected_graph.png" | relative_url}}){:height="300" width="400"}

  - 방향 그래프(Directed Graph)
    + 간선에 방향이 있는 그래프
    + 노드 A->B로 가는 간선이 있을 경우 <A,B>로 표기   
      + <B,A> 와 <A,B>는 다른 것   

  ![directed_graph]({{"/assets/img/algorithm/graph/directed_graph.png" | relative_url}}){:height="300" width="400"}

* 가중치 그래(Weighted Graph)
  - 간선에 비용 또는 가중치가 할당된 그래프
  - 네트워크(Network)라고도 함
  
  ![weighted_graph]({{"/assets/img/algorithm/graph/weighted_graph.png" | relative_url}}){:height="300" width="400"}

* 연결 그래프 vs 비연결 그래프
  - 연결 그래프(Connected Graph)
    + 무방향 그래프에 있는 모든 노드에 대해 항상 경로가 존재하는 경우

  - 비연결 그래프(Disconnected Graph)
    + 무방향 그래프에서 특정 노드에 대해 경로가 존재하지 않는 경우   

  ![disconnected_graph]({{"/assets/img/algorithm/graph/disconnected_graph.png" | relative_url}}){:height="300" width="400"}

* 사이클과 비순환 그래프
  - 사이클(Cycle)
    + 단순 경로의 시작노드와 종료 노드가 동일한 경우

  - 비순환 그래프(Acyclic Graph)
    + 사이클(Cycle)이 없는 그래프

  ![acyclic_graph]({{"/assets/img/algorithm/graph/acyclic_graph.png" | relative_url}}){:height="300" width="400"}

* 완전 그래프(Complete Graph)
  - 그래프의 모든 노드가 서로 연결되어 있는 그래프
  - 정점의 수 : n
  - 간선의 수 : n * (n-1) / 2

  ![complete_graph]({{"/assets/img/algorithm/graph/complete_graph.png" | relative_url}}){:height="300" width="400"}


### 4. 그래프(Graph)와 트리(Tree)의 차이

* 트리는 그래프 중에 한 종류   

||그래프|트리|
|---|:---:|:---:|
| 정의 | 노드와 노드를 연결하는 간선으로 표현된 자료구조 | 그래프의 한 종류로 방향성이 있는 비순환 그래프|
| 방향성 | 방향그래프, 무방향그래프 | 방향 그래프 |
| 사이클 | 순환 및 비순환 그래프 | 비순환 그래프이므로 사이클이 존재하지 않음 |
| 루트 노드 | 루트 노드가 존재하지 않음 | 루트 노드 존재 |
| 부모/자식 관계 | 부모 자식 개념이 존재하지 않음 | 부모 자식 관계가 존재함 |


---------------------------------------------------------------
## 참고자료
> * <https://fun-coding.org>
