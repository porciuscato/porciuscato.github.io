---
title: 크루스칼 알고리즘
published: true
updated: 2020-5-23
tags: [python, algorithm, graph, disjoint-set, mst, kruskal]
categories: [development]
---

프림 알고리즘에 대해 알아보자.

크루스칼 알고리즘에 대해 알아보자.



## 크루스칼 알고리즘

> 최소 가중치 간선을 하나씩 선택해서 최소 신장 트리를 찾는 알고리즘

- N개의 정점을 포함하는 그래프에서 n -1 개의 간선을 선택하는 방식

- 간선을 선택해 나가는 과정에 여러 개의 트리들이 존재

  - 초기 상태는 n개의 정점들이 각각 하나의 트리가 됨

    -> 하나의 정점을 포함하는 n 개의 상포 배타 집합 존재

  - 간선을 선택하면 간선의 두 정점이 속한 트리가 연결되고 하나의 집합으로 합쳐짐

  - 선택한 간선의 두 정점이 이미 연결된 트리에 속한 정점들일 경우 사이클이 생김 

    -> 두 정점에 대해 같은 집합의 원소 여부 검사



### 동작 과정

1. 최초, 모든 간선을 가중치에 따라 오름차순으로 정렬
2. 가중치가 가장 낮은 간선부터 선택하면서 트리 증가시킴
   - 사이클이 존재하면 다음으로 가중치가 낮은 간선 선택
3. n-1개의 간선이 선택될 때까지 두 번째 과정을 반복

```python
def MST_KRUSKAL(G):
    mst = []
    
    for i in range(N):
        Make_Set(i)
        
    G.sort(key=lambda t: t[2])				# 가중치 기준으로 정렬
    
    mst_cost = 0							# MST 가중치
    
    while len(mst) < N-1:
        u, v, val = G.pop(0)				# 최소 가중치 간선 가져오기
        if Find_Set(u) != Find_Set(v):
            Union(u, v)
            mst.append((u, v))				# 트리에 (u, v) 추가
            mst_cost += val
```





#### 특징

- 간선 선택 과정에서 생성되는 트리를 관리하기 위해 상호 배타 집합 사용
  - 트리에 속한 노드들은 자신을 루트로 하는 서브트리의 높이를 랭크라는 이름으로 저장
- 선택한 간선으로 두 개의 트리가 한 개의 트리로 합쳐질 때 각 트리에 해당하는 상호 배타 집합을 Union 연산으로 합침
  - 랭크 값이 작은 트리를 랭크 값이 큰 트리의 서브트리로 포함시킬 경우 트리에 포함된 노드들의 랭크 값 수정 불필요



### \+ disjoint_set

```python
def make_set(x):
    parent[x] = x
    rank[x] = 0


def find_set(x):
    if x != parent[x]:
        parent[x] = find_set(parent[x])
    return parent[x]


def link(x, y):
    if rank[x] >= rank[y]:
        parent[y] = x
    else:
        parent[x] = y
    if rank[x] == rank[y]:
        rank[x] += 1


def union(x, y):
    link(find_set(x), find_set(y))
```

