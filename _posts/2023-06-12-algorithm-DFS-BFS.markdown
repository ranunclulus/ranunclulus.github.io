---
layout: post
title:  "Algorithm 3 DFS/BFS"
date:   2023-06-12 14:18:38 +0900
categories: jekyll update
---

## DFS/BFS

### DFS

- Depth-First Search
- 깊이 우선 탐색
- 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
- 자료구조 중 [스택](https://www.notion.so/Data-Structure-1-Stack-b82fb9044b7648cf9249a2df2c6fea41?pvs=21)을 활용하여 구현
- 시간 복잡도 O(N)
- DFS 방문 순서는 고정적이지 않음
  - 노드의 방문 순서는 탐색하는 경로에 따라 달라짐
  - DFS의 방문 순서는 스택에서 노드를 꺼내는 순서에 따라 결정
  - DFS에서 방문 순서는 알고리즘의 구현 방식, 시작 노드, 그래프의 구조 등에 따라 달라질 수 있음

### Process

- 시작 노드를 스택에 push 하고 방문 처리
- 스택에서 노드를 pop
- 해당 노드와 인접한 노드 중 아직 방문하지 않은 노드가 있다면 스택에 push 하고 방문 처리
- 2-3 과정을 반복
- 스택이 빌 때까지 2-4 과정을 반복

### Example

- 시작 노드가 1인 그래프 DFS 동작하기

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/GAxqb/btqJ6dAYOOz/p3ysI6YO2vKBtydazxsHW1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/GAxqb/btqJ6dAYOOz/p3ysI6YO2vKBtydazxsHW1/img.png)

- 시작 노드인 1을 스택에 넣고 방문 처리

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/VJVxF/btqJ4HCmJ5l/pwWKCcQB3Akn6186o3VWXk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/VJVxF/btqJ4HCmJ5l/pwWKCcQB3Akn6186o3VWXk/img.png)

- 노드 1과 인접해 있지만 방문하지 않은 노드 2, 3, 8 중 가장 작은 2를 넣고 방문 처리

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/oJ4ex/btqJWRNcBZm/mXHsEc5wVRNfbFVIYOMxw1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/oJ4ex/btqJWRNcBZm/mXHsEc5wVRNfbFVIYOMxw1/img.png)

- 2의 인접 노드 1, 7 중 방문하지 않은 노드 7을 넣고 방문 처리

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/mo5iW/btqJWRNcB1w/H1GLVZUl837r4okMVDHZj0/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/mo5iW/btqJWRNcB1w/H1GLVZUl837r4okMVDHZj0/img.png)

- 7의 인접 노드 6, 8 중 방문하지 않고 가장 작은 6을 넣고 방문 처리

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/cv2RBz/btqJ3hcOqeI/N0RUrpScWG5whJjymGOsL1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/cv2RBz/btqJ3hcOqeI/N0RUrpScWG5whJjymGOsL1/img.png)

- 6의 인접 노드 7 중 방문하지 않은 노드가 없기에 6을 꺼냄

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/b910J3/btqJ0oQ5VLP/SEHo4XvRsUCzK3oPLkzdlk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/b910J3/btqJ0oQ5VLP/SEHo4XvRsUCzK3oPLkzdlk/img.png)

- 7의 인접 노드 6, 8 중 방문하지 않은 노드 8 넣고 방문 처리

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/l2ML8/btqJ8gxr1Qe/mgvbwo0GKlAkKGhaeKtxR1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/l2ML8/btqJ8gxr1Qe/mgvbwo0GKlAkKGhaeKtxR1/img.png)

- 결과적으로 노드의 탐색 순서 (스택에 들어간 순서): 1 → 2 → 7 → 6 → 3 → 4 → 5

### Implementation

```python
visited = [False] * 9

def dfs(graph, v, visited):
    #graph: 그래프
    #v: 시작 노드
    #visited: 방문 정보
    visited[v] = True
    #print(v, end=" ")
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

# Non Recursive approach
def Non_Recursive_dfs(graph, v):
    path = []
    stack = []
    stack.append(v)

    while stack:
        s = stack.pop()
        if s not in path:
            path.append(s)

        if s in path:
            #leaf node
            continue
        for neighbour in graph[s]:
            stack.append(neighbour)

    return " ".join(path)
```

---

### BFS

- Breadth-First Search
- 너비 우선 탐색
- 그래프에서 시작 노드로부터 같은 레벨의 노드들을 먼저 방문하고 다음 레벨의 노드를 방문하는 알고리즘
- 자료구조 중 [큐](https://www.notion.so/Data-Structure-2-Queue-85e13d4c893e40ae9bfddc476761984a?pvs=21)을 활용하여 구현
- 시간 복잡도 O(N)
- BFS 방문 순서는 같은 그래프에서는 항상 같은 순서로 방문함
  - 하지만 만약 그래프에 여러 개의 최단 경로가 있다면 BFS는 다양한 방식으로 노드를 탐색할 수 있기에 방문 순서가 다를 수 있음

### Process

- 시작 노드를 큐에 enqueue하고 방문 처리
- 큐에서 dequeue를 하고 해당 노드의 인접 노드 중 방문하지 않은 노드를 모두 enqueue한 뒤 방문 처리
- 해당 노드와 인접한 노드 중 아직 방문하지 않은 노드가 있다면 스택에 push 하고 방문 처리
- 2-3 과정을 반복

### Example

- 시작 노드가 1인 그래프 BFS 동작하기

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/GAxqb/btqJ6dAYOOz/p3ysI6YO2vKBtydazxsHW1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/GAxqb/btqJ6dAYOOz/p3ysI6YO2vKBtydazxsHW1/img.png)

- 시작 노드인 1을 큐에 넣고 방문 처리

  ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/VJVxF/btqJ4HCmJ5l/pwWKCcQB3Akn6186o3VWXk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/VJVxF/btqJ4HCmJ5l/pwWKCcQB3Akn6186o3VWXk/img.png)

- 노드 1을 꺼내고 방문하지 않은 인접 노드 2, 3, 8 을 큐에 넣은 뒤 방문 처리

  ![https://velog.velcdn.com/images/morion002/post/4678b53b-ff53-4eba-a14c-ba227426cdb3/image.png](https://velog.velcdn.com/images/morion002/post/4678b53b-ff53-4eba-a14c-ba227426cdb3/image.png)

- 노드 2를 꺼내고 방문하지 않은 인접 노드 7을 넣은 뒤 방문 처리

  ![https://velog.velcdn.com/images/morion002/post/008c38ee-a77b-4228-a790-aae4701498b3/image.png](https://velog.velcdn.com/images/morion002/post/008c38ee-a77b-4228-a790-aae4701498b3/image.png)

- 노드 3을 꺼내고 방문하지 않은 인접 노드 4, 5을 큐에 넣은 뒤 방문 처리

  ![https://velog.velcdn.com/images/morion002/post/6d948265-70ae-4d85-8418-491e99b32e96/image.png](https://velog.velcdn.com/images/morion002/post/6d948265-70ae-4d85-8418-491e99b32e96/image.png)

- 노드 8을 꺼내고 방문하지 않은 인접 노드 없기 때문에 패스

  ![https://velog.velcdn.com/images/morion002/post/6602a298-5388-46de-8652-3ebc14c104a0/image.png](https://velog.velcdn.com/images/morion002/post/6602a298-5388-46de-8652-3ebc14c104a0/image.png)

- 노드 7을 꺼내고 방문하지 않은 인접 노드인 6을 큐에 넣고 방문 처리

  ![https://velog.velcdn.com/images/morion002/post/9a2c7233-47e3-4906-a1f1-c520370349e8/image.png](https://velog.velcdn.com/images/morion002/post/9a2c7233-47e3-4906-a1f1-c520370349e8/image.png)

- 이 과정을 반복한 탐색 순서는 1 → 2 → 3 → 8 → 7 → 4 → 5 → 6

### Implementation

```python
from collections import deque

visited = [False] * 9

def bfs(graph, start, visited):
    #graph: 그래프
    #start: 시작 노드
    #visited: 방문 정보
    queue = deque([start])
    visited[start] = True
    while queue:
        v = queue.popleft()
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True
```

## Exercise

### 음료수 얼려 먹기

- 문제
  - N × M 크기의 얼음 틀이 있음
  - 구멍이 뚫려 있는 부분은 0, 칸막이가 존재하는 부분은 1로 표시
  - 구멍이 뚫려 있는 부분끼리 상, 하, 좌, 우로 붙어 있는 경우 서로 연결되어 있는 것으로 간주
  - 이때 얼음 틀의 모양이 주어졌을 때 생성되는 총 아이스크림의 개수를 구하는 프로그램을
  - 다음의 4 × 5 얼음 틀 예시에서는 아이스크림이 총 3개가 생성
- 입력
  - 첫 번째 줄에 얼음 틀의 세로 길이 N과 가로 길이 M (1 <= N, M <= 1,000)
  - 두 번째 줄부터 N + 1 번째 줄까지 얼음 틀의 형태가 주어짐
  - 이때 구멍이 뚫려있는 부분은 0, 그렇지 않은 부분은 1
- 문제 해설
  - 특정한 지점의 주변 상, 하 좌, 우를 살펴본 뒤에 주변 지점 중에서 값이 0이면서 아직 방문하지 않은 곳 방문
  - 그 지점에서 다시 상, 하, 좌, 우를 살피다가 주변에 1로 막혀 있는 곳이 있다면 재귀 끝
  - 하나의 영역이 하나의 카운트가 되는 방법

```python
n, m = map(int, input().split())

graph = []
for i in range(n):
    graph.append(list(map(int, input())))

def dfs(x, y):
    if x <= -1 or x >= n or y <= -1 or y >= m:
        return False
    if graph[x][y] == 0:
        graph[x][y] = 1
        dfs(x-1, y)
        dfs(x+1, y)
        dfs(x, y-1)
        dfs(x, y+1)
        return True
    return False

result = 0
for i in range(n):
    for j in range(m):
        if dfs(i, j) == True:
            result += 1

print(result)

```

### 미로 탈출

- 문제
  - N x M 크기의 직사각형 형태의 미로에 여러 마리의 괴물이 있어 이를 피해 탈출해야 함
  - 현재 위치는 (1, 1)이고 미로의 출구는 (N,M)의 위치에 존재하며 한 번에 한 칸씩 이동할 수 있음
  - 괴물이 있는 부분은 0으로, 괴물이 없는 부분은 1로 표시
  - 미로는 반드시 탈출할 수 있는 형태로 제시
  - 탈출하기 위해 움직여야 하는 최소 칸의 개수
  - 칸을 셀 때는 시작 칸과 마지막 칸을 모두 포함해서 계산
- 입력 조건
  - 첫째 줄에 두 정수 N, M(4 <= N, M <= 200)이 주어짐
  - 다음 N개의 줄에는 각각 M개의 정수(0혹은 1)로 미로의 정보가 주어짐
  - 각각의 수들은 공백 없이붙어서 입력으로 제시
  - 또한 시작 칸과 마지막 칸은 항상 1
- 출력 조건
  - 첫째 줄에 최소 이동 칸의 개수를 출력

```python
from collections import deque

n, m = map(int, input().split())
result = 1
graph = []
for i in range(n):
    graph.append(list(map(int, input())))

dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

def bfs(x, y):
    queue = deque()
    queue.append((x, y))
    while queue:
        x, y = queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if nx < 0 or ny < 0 or nx >= n or ny >= m:
                continue
            if graph[nx][ny] == 0:
                continue
            if graph[nx][ny] == 1:
                #현재 탐색 위치에 여태까지 몇 칸을 짚고 왔나 저장
                graph[nx][ny] = graph[x][y] + 1
                queue.append((nx, ny))
    return graph[n-1][m-1]

print(bfs(0, 0))
```