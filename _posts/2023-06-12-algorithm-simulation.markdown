---
layout: post
title:  "Algorithm 2 Simulation"
date:   2023-06-12 14:17:38 +0900
categories: jekyll update
---

## Simulation Algorithm

### Simulation

- 머릿속에 있는 알고리즘을 소스 코드로 바꾸는 과정
- 풀이를 떠올리는 것은 쉽지만 소스 코드로 옮기는 것은 어려운 문제
- 완전 탐색: 모든 경우의 수를 주저 없이 다 계산하는 방법
- 시뮬레이션: 문제에서 제시한 알고리즘을 한 단게씩 차례대로 직접 수행해야 하는 문제 유형

## Exercise

### 상하좌우

- 문제
  - 여행가 A는 NxN 크기의 정사각형 공간에 서 있고, 이 공간은 1 x 1 크기의 정사각형으로 나누어져 있음 가장 왼쪽 위 좌표는 (1, 1)이고 가장 오른쪽 아래 좌표는 (N, N)이다.상하좌우로 이동할 수 있으며, 시작 좌표는 (1,1)
  - 계획서대로 이동하면 되는데L, R, U, D는 각각 왼쪽, 오른쪽, 위, 아래로 한칸씩 이동하라는 뜻
  - 만약 공간을 벗어나는 움직임이 있다면 그 움직임은 무시하고 다음으로 넘어감
- 입력 조건
  - 첫째 줄에 공간의 크기를 나타내는 N이 주어짐
  - 둘째 줄에 여행가 A가 이동할 게획서 내용 주어짐
- 출력 조건
  - 첫째 줄에 여행가 A가 최종적으로 도착할 지점의 좌표를 공백으로 구분하여 출력

```python
def solution():
	n = int(input())
	root = input().split()
	move = {"L":0,
					"R":1,
					"U":2,
					"D":3}
	move_x = [0, 0, -1, 1]
	move_y = [-1, 1, 0, 0]
	x = 1
	y = 1
	for r in root:
		index = move[r]
		nx = x + move_x[index]
		ny = y + move_y[index]
		if nx >= 1 and ny >= 1 and nx <= n and ny <= n :
			x = nx
			y = ny
	print(x, y)
```

```python
#답안 예시
n = int(input())
x, y = 1, 1
plans = input().split()
#L, R, U, D에 따른 이동 방향
dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]
move_types = ['L', 'R', 'U', 'D']
#이동 계획을 하나씩 확인
for plan in plans:
	for i in range(len(moge_types)):
		if plan == move_types[i]:
			nx = x + dx[i]
			ny = y + dy[i]
		if nx < 1 or ny < 1 or nx > n or ny > n :
			continue
		x, y = nx, ny
print(x, y)
```

### 시각

- 문제
  - 정수 N이 입력되면 00시 00분 00초부터 N시 59분 59초까지 모둔 시각 중 3이 하나라도 포함되는 모든 경우의 수 구하기
- 입력 조건
  - 첫째 줄에 정수 N이 주어짐
- 출력 조건
  - 00시 00분 00초부터 N시 59분 59초까지 모둔 시각 중 3이 하나라도 포함되는 모든 경우의 수 출력

```python
def solution():
	result = 0
	n = int(input())
	for h in range(n+1):
		for m in range(60):
			for s in range(60):
				time = str(h) + " "+ str(m) + " " + str(s)
				if '3' in time:
					result += 1
	return result
```

```python
h = int(input())

count = 0
for i in range(h+1):
	for j in range(60):
		for k in range(60):
			if '3' in str(h) + str(m) + str(s):
				count += 1
print(count)
```

## Practice

### 왕실의 나이트

- 문제
  - 행복 왕국의 왕실 정원은 체스판과 같은 8 × 8 좌표 평면
  - 왕실 정원의 특정한 한 칸에 나이트가 서 있음
  - 나이트는 말을 타고 있기 때문에 이동을 할 때는 L자 형태로만 이동할 수 있으며 정원 밖으로는 나갈 수 없음
  - 나이트는 특정 위치에서 다음과 같은 2가지 경우로 이동할 수 있음
  - 수평으로 두 칸 이동한 뒤에 수직으로 한 칸
  - 수직으로 두 칸 이동한 뒤에 수평으로 한 칸

    !https://velog.velcdn.com/images%2Fsuzieep%2Fpost%2Fc01d7972-7c64-400b-a07c-664bb10ebc88%2Fimage.png

  - 이처럼 8 × 8 좌표 평면상에서 나이트의 위치가 주어졌을 때 나이트가 이동할 수 있는 경우의 수를 출력하는프로그램을 작성
  - 왕실의 정원에서 행 위치를 표현할 때는 1부터 8로 표현하며, 열 위치를 표현할 때는a 부터 h로 표현한
  - c2에 있을 때 이동할 수 있는 경우의 수는 6가지
  - a1에 있을 때 이동할 수 있는 경우의 수는 2가지
- 입력 조건
  - 첫째 줄에 8x8 좌표 평면 상에서 현재 나이트가 위치한 곳의 좌표를 나타내는 두 문자로 구성된 문자열이 입력
  - 입력 문자는 a1 처럼 열과 행으로 이뤄짐
- 출력 조건
  - 첫째 줄에 나이트가 이동할 수 있는 경우의 수

```python
#멍청한 풀이
def solution():
  temp = input()
  result = 0
  x, y = ord(temp[0])-96, int(temp[1])
  if x+2 < 9:
    if y+1 <9:
      result += 1
    if y-1 >0:
      result += 1
  if x-2 >0:
    if y+1 <9:
      result += 1
    if y-1 >0:
      result += 1
  if y+2 < 9:
    if x+1 <9:
      result += 1
    if x-1 >0:
      result += 1
  if y-2 >0:
    if x+1 <9:
      result += 1
    if x-1 >0:
      result += 1
  return result

```

```python
#좌표를 이용한 풀이
def solution():
  temp = input()
  result = 0
  x, y = ord(temp[0])-96, int(temp[1])
  dx = [-1, 1, 2, 2, 1, -1, -2, -2]
  dy = [2, 2, 1, -1, -2, -2, -1, 1]
  for i in range(8):
    nx, ny = x + dx[i], y + dy[i]
    if nx < 1 or ny < 1 or nx > 8 or ny > 8:
      continue
    else:
      result += 1
  return result

```

### 게임 개발

- 문제
  - 현민이는 게임 캐릭터가 맵 안에서 움직이는 시스템을 개발 중
  - 캐릭터가 있는 장소는 1X1 크기의 정사각형으로 이뤄진 NXM 크기의 직사각형으로, 각각의 칸은 육지 또는 바다
  - 캐릭터는 동서남북 중 한 곳을 바라봄
  - 맵의 각 칸은 (A, B)로 나타낼 수 있고, A는 북쪽을부터 떨어진 칸의 개수, B는 서쪽으로부터 떨어진 칸의 개수
  - 캐릭터는 상하좌우로 움직일 수 있고, 바다로 되어 있는 공간에는 갈 수 없다
  - 캐릭터의 움직임을 설정하기 위해 정해 높은 매뉴얼은 아래와 같음
    1. 현재 위치에서 현재 방향을 기준으로 왼쪽 방향(반시계 방향으로 90도 회전한 방향)부터 차례대로 갈 곳을 정함
    2. 캐릭터의 바로 왼쪽 방향에 아직 가보지 않은 칸이 존재한다면, 왼쪽 방향으로 회전한 다음 왼쪽으로 한 칸을 전진 왼쪽 방향에 가보지 않은 칸이 없다면, 왼쪽 방향으로 회전만 수행하고 1단계로 돌아감
    3. 만약 네 방향 모두 이미 가본 칸이거나 바다로 되어 있는 칸인 경우에는, 바라보는 방향을 유지한 채로 한 칸 뒤로 가고 1단계로 돌아감 이때 뒤쪽 방향이 바다인 칸이라 뒤로 갈 수 없는 경우에는 움직임을 멈춤
  - 현민이는 위 과정을 반복적으로 수행하면서 캐릭터의 움직임에 이사잉 있는지 테스트하고자 함
  - 매뉴얼에 따라 캐릭터를 이동시킨 뒤에, 캐릭터가 방문한 칸의 수를 출력하는 프로그램
- 입력 조건
  - 첫째 줄에 맵의 세로 크기 N과 가로 크기 M을 공백으로 구분하여 입력 (3<=N,M<=50)
  - 둘째 줄에 게임 캐릭터가 있는 칸의 좌표 (A, B)와 바라보는 방향 d가 각각 서로 공백으로 구분하여 주어짐
  - 방향 d의 값으로는 다음과 같이 4가지가 존재
    - 0 : 북쪽
    - 1 : 동쪽
    - 2 : 남쪽
    - 3 : 서쪽
  - 셋째 줄부터 맵이 육지인지 바디인지에 대한 정보가 주어짐
  - N개의 줄에 맵의 상태가 북쪽부터 남쪽 순서대로, 각 줄의 데이터는 서쪽부터 동쪽 순서대로 주어짐
  - 맵의 외곽은 항상 바다로 되어 있음
    - 0 : 육지
    - 1 : 바다
  - 처음에 게임 캐릭터가 위치한 칸의 상태는 항상 육지
- 출력 조건
  - 첫째 줄에 이동을 마친 후 캐릭터가 방문한 칸의 수를 출력한다

```python
def solution():
  n, m = map(int, input().split())
  x, y, dir = map(int, input().split())
  array = []
  for i in range(n):
    array.append(list(map(int, input().split())))
  dx = [-1, 0, 1, 0]
  dy = [0, -1, 0, 1]
  count = 1

  for i in range(4):
    dir = (dir + i + 3) % 4
    nx, ny = x + dx[dir], y + dy[dir]
    if nx >= 0 and ny >= 0 and nx <= n and ny <= m and array[nx][ny] == 0 :
      x, y = nx, ny
      array[x][y] = 1
      count += 1
      i = 0
  return count
```

```python
n, m = map(int, input().split())
d = [[0] * m for _ in range(n)]
x, y, direction = map(int, input().split()) # 현재 캐릭터의 X좌표, Y좌표, 방향 입력받기
d[x][y] = 1 # 현재 좌표 방문 처리

array = []
for _ in range(n):
    array.append(list(map(int, input().split()))) # 전체 맵 정보

dx = [-1, 0, 1, 0] # 북, 동, 남, 서 방향 정의
dy = [0, 1, 0, -1]

def turn_left(): # 왼쪽으로 회전
    global direction
    direction -= 1
    if direction == -1:
        direction = 3

# 시뮬레이션 시작
count = 1
turn_time = 0
while True:
    turn_left()
    nx = x + dx[direction]
    ny = y + dy[direction]

    # 회전한 이후 정면에 가보지 않은 칸이 없거나 바다인 경우
    if d[nx][ny] == 0 and array[nx][ny] == 0:
        d[nx][ny] = 1
        x = nx
        y = ny
        count += 1
        turn_time = 0
        continue

    else:
        turn_time += 1

    # 네 방향 모두 갈 수 없는 경우
    if turn_time == 4:
        nx = x - dx[direction]
        ny = y - dy[direction]

        # 뒤로 갈 수 있다면
        if array[nx][ny] == 0:
            x = nx
            y = ny
        # 뒤가 바다라면
        else:
            break
        turn_time = 0

print(count)
```