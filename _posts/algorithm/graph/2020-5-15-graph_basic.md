---
title: 그래프 기본
published: true
updated: 2020-5-15
tags: [python, algorithm, mst, prim, kruskal, dijkstra, graph]
categories: [development]
---

그래프의 탐색



## 그래프 탐색

=> 그래프 순회: DFS / BFS



### DFS(Depth First Search)

- 시작 정점에서 갈 수 있는 한 방향을 선택해서 다음 정점으로 이동
- 선택된 정점에서 다시 위와 같은 작업을 반복 수행하면서 갈 수 있는 경로가 있는 곳까지 깊이 탐색
  - 이미 방문했던 정점은 재방문하지 않음
- 더이상 갈 곳이 없으면 가장 최근에 방문한 갈림길이 있는 정점으로 되돌아가서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법

\* **스택** or **재귀** 사용



#### 재귀 사용

```python
# G: 그래프, v: 정점
# visited: 방문처리
# G[v]: 그래프 G에서 v의 인접 정점 리스트

def dfs(G, v):
    visited[v] = True
    for w in G[v]:
        if not visited[w]:
            dfs(G, W)
```



#### 스택 사용

```python
def dfs(stack, v):
    stack = [v]
    while stack:
        ele = stack.pop() # 맨 위의 정점을 빼낸다.
        if ele not in visited:
            visited.append(ele)
            visit() # 처리
            stack.extend(G[v] - set(visited))
    return visited
```





### BFS (Breath First Search)

- 탐색 시작점의 인접한 정점들을 먼저 모두 차례로 방문
- 방문했던 정점들을 다시 시작점으로 하여 앞의 과정을 반복 수행

\* 인접한 정점들에 대해 탐색 -> 차례로 너비 우선 탐색 진행

\* **큐**를 사용

#### 큐 사용

```python
visited = [0] * N # 정점의 개수
D = [0] * N
P = [0] * N

def bfs(que, v):
    que = [v]
    visited[v] = True
    visit(v) # 처리
    while que:
        ele = que.pop(0) # 첫 번째 정점을 꺼낸다.
        for w in G[v]:
            if not visited[w]:
                que.append(w)
                visited[w] = True
                visit(v) # 처리
```

<table>
    <thead>
        <tr>
    		<th>정점</th>
            <th>1</th>
            <th>2</th>
            <th>3</th>
            <th>4</th>
            <th>5</th>
            <th>6</th>
            <th>7</th>
            <th>8</th>
        </tr>
    </thead>
	<tbody>
        <tr>
            <th>방문정보</th>
            <td>T</td><td>T</td><td>T</td><td>T</td>
            <td>T</td><td>T</td><td>T</td><td>T</td>
        </tr>
        <tr>
            <th>거리(D)</th>
            <td>0</td><td>1</td><td>1</td><td>2</td>
            <td>1</td><td>2</td><td>2</td><td>3</td>
        </tr>
        <tr>
            <th>경로(P)</th>
            <td>1</td><td>1</td><td>1</td><td>2</td>
            <td>1</td><td>2</td><td>5</td><td>6</td>
        </tr>
	</tbody>
</table>

> 거리는 1번 정점으로부터의 거리
>
> 경로는 부모 정점

\* 경로를 타고 가면 해당 정점에서 1번으로 가는 최단거리를 구할 수 있다.


