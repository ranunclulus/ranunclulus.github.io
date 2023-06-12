---
layout: post
title:  "Algorithm 1 Greedy"
date:   2023-06-12 14:06:38 +0900
categories: jekyll update
---

## Greedy Algorithm

### Greedy

- 현재 상황에서 지금 당장 좋은 것만 고르는 방법
- 매 순간 가장 좋아 보이는 것을 선택
- 현재의 선택이 나중에 미칠 영향에 대해 고려하지 않음
- 기준에 따라 좋은 것을 선택하는 알고리즘으로, 기준을 제시하는 경우 많음
- 문제 풀이를 위한 최소한의 아이디어를 떠올리고, 이것이 정당한지 검토할 수 있어야 답 도출 가능

## Exercise

### 거스름돈

- 문제
  - 카운터에는 거스름돈으로 사용할 500원, 100원, 50원, 10원짜리 동전이 무한히 존재
  - 손님에게 거슬러 줘야 할 돈이 N원일 때 거슬러 줘야 할 동전의 최소 개수
- 문제 해설
  - 가장 큰 화폐 단위부터 돈을 거슬러 주는 것
  - ex) 1260원의 거스름돈이 존재할 때, 500\*2 + 100\*2 + 50\*1 + 10\*1

```python
def solution(change):
	cnt = 0
    coin_types = [500, 100, 50, 10]
    for coin in coin_tyes:
    	cnt += change // coin
        change = change % coin
    return change

```

## Practice

### 큰 수의 법칙

- 문제
  - 다양한 수로 이루어진 배열이 있을 때 주어진 수들을 M번 더하여 가장 큰 수를 만드는 법칙
  - 단 배열의 특정한 인덱스에 해당하는 수가 연속해서 K번을 초과하여 더해질 수 없음
  - 서로 다른 인덱스이 경우 해당하는 수가 같아도 서로 다른 수라고 간주
  - 예를 들어 순서대로 2, 4, 5, 4, 6으로 이루어진 배열이 있을 때 M이 8이고, K가 3이라고 가정하는 경우 큰 수의 법칙에 따른 결과는 6 + 6 + 6 + 5 + 6 + 6 + 6 + 5인 46
- 입력 조건
  - 첫째 줄에 N, M, K의 자연수가 주어지며, 각 자연수는 공백으로 구분
  - 둘째 줄에 N개의 자연수가 주어지며 각 자연수는 공백으로 구분
  - 입력으로 주어지는 K는 M보다 항상 작거나 같음
- 출력 조건
  - 큰 수의 법칙에 따라 더해진 답

```python
# 풀이 1
def solution():
    result = 0
    n, m, k = map(int, input().split())
    numbers = list(map(int, input().split()))
    numbers.sort(reverse=True)

    j = 0
    for i in range(m):
        if j < k:
            result += numbers[0]
            j += 1
        elif j == k:
            j = 0
            result += numbers[1]
    return result

  # 풀이 2
  def solution():
    result = 0
    n, m, k = map(int, input().split())
    numbers = list(map(int, input().split()))
    numbers.sort(reverse=True)
    first = numbers[0]
    second = numbers[1]
    count = int(m / (k + 1)) * k
    count += m % (k + 1)
    return first * count + second * (m - count)

```

### 숫자 카드 게임

- 문제
  - 숫자가 쓰인 카드들이 n\*m 형태로 놓여 있음 (이때 n은 행의 개수, m은 열의 개수)
  - 먼저 뽑고자 하는 카드가 포함되어 있는 행 선택
  - 그다음 선택된 행에 포함된 카드들 중 가장 숫자가 낮은 카드 뽑기
  - 따라서 처음에 카드를 골라낼 행을 선택할 때, 이후에 해당 행에서 가장 숫자가 낮은 카드를 뽑을 것을 고려하여 최종적으로 가장 높은 숫자의 카드를 뽑을 수 있도록 전략 구성 필요
- 입력 조건
  - 첫째 줄에 숫자 카드들이 놓인 행의 개수 n과 열의 개수 m이 공백을 기준으로 하여 각각 자연수로 주어짐
  - 둘째 줄부터 n개의 줄에 걸쳐 각 카드에 적힌 숫자가 주어짐
- 출력 조건
  - 첫째 줄에 게임의 룰에 맞게 선택한 카드에 적힌 숫자 출력

```python
# 풀이 1
def solution():
    n, m = map(int, input().split())
    arr = []
    for _ in range(n):
        arr.append(list(map(int, input().split())))
    temp = []
    for i in range(n):
        temp.append(min(arr[i]))
    return(max(temp))

# 풀이 2
def solution():
    n, m = map(int, input().split())
    result = 0
    for _ in range(n):
        data = list(map(int, input().split()))
        min_val = min(data)
        result = max(min_val, result)
    return result

```

### 1이 될 때까지

- 문제
  - 어떤 수 n이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 수행
    - n에서 1을 뺀다
    - n을 k로 나눈다
  - n이 1이 될 때까지 1번 혹은 2번의 과정을 수행해야 하는 횟수의 최솟값 구하기
- 입력 조건
  - 첫째 줄에 n과 k가 공백으로 구분되며 각각 자연수로 주어짐
- 출력 조건
  - 첫째 줄에 n이 1이 될 때까지 1번 혹은 2번의 과정을 수행해야 하는 횟수의 최솟값을 출력

```python
# 풀이 1
def solution():
    n, k = map(int, input().split())
    cnt = 0
    while(n != 1):
        if(n % k != 0):
            n -= 1
            cnt += 1
        else:
            n /= k
            cnt += 1
    return cnt

  # 풀이 2
  def solution():
    n, k = map(int, input().split())
    result = 0
    while True:
        # (n == k로 나누어떨어지는 수)가 될 때까지 1씩 빼기
        target = (n//k) * k
        result += (n - target)
        n = target
        # n이 k보다 작을 때(더 이상 나눌 수 없을 때) 반복문 탈출
        if n < k:
            break
        # k로 나누기
        result += 1
        n //= k
    # 마지막으로 남은 수에 대하여 1씩 빼기
    result += (n - 1)
    return result

```

## Test

### 볼링공 고르기

- 문제
  - A, B 두 사람이 볼링을 치고 있음
  - 두 사람은 서로 무게가 다른 볼링공을 고르려고 함
  - 볼링공은 총 n개가 있으며 각 볼링공마다 무게가 적혀 있고, 공의 번호는 1번부터 순서대로 부여됨
  - 같은 무게의 공이 여러 개 있을 수 있지만, 서로 다른 공으로 간주
  - 볼링공의 무게는 1부터 M까지 자연수 형태로 존재
  - n개의 공의 무게가 각각 주어질 때, 두 사람이 볼링공을 고르는 경우의 수 반환
- 예시
  - n=5, m=3일 때
  - 볼링공의 무게는 각각 차례로 1, 3, 2, 3, 2
  - (1, 2), (1, 3), (1, 4), (1, 5), (2, 3), (2, 5), (3, 4), (4, 5)
  - 총 여덟 가지의 경우의 수 가능
- 입력 조건
  - 첫째 줄에 볼링공의 개수 n, 공의 최대 무게 m이 공백으로 구분되어 각각 자연수 형태로 주어짐
  - 둘째 줄에 각 볼링공의 무게 k가 공백으로 구분되어 순서대로 자연수 형태로 주어짐

```python
# 풀이 1
def solution():
    n, m = map(int, input().split())
    balls = list(map(int, input().split()))
    result = 0
    for i in range(n):
        for j in range(n):
            if i != j and balls[i] != balls[j]:
                result += 1
    return (result//2) # 중복되는 조합 제거

```

- 해설 (문제에 주어진 예시 사용)
  - 무게마다 볼링공이 몇 개 있는지 계산
    - 무게가 1인 볼링공: 1개
    - 무게가 2인 볼링공: 2개
    - 무게가 3인 볼링공: 2개
  - A가 특정한 무게의 볼링공을 선택했을 때, 이어서 B가 볼링공을 선택하는 경우를 차례대로 계산하여 문제 해결
  - A를 기준으로 무게가 낮은 볼링공부터 무게가 높은 볼링공까지 순서대로 하나씩 확인했을 경우
    - A가 무게가 1인 공을 선택할 때의 경우의 수 = 1(무게가 1인 공의 개수) * 4(B가 선택하는 경우의 수) = 4
    - A가 무게가 2인 공을 선택할 때의 경우이 수 = 2(무게가 2인 공의 개수) * 2(B가 선택하는 경우의 수) = 4
    - A가 무게가 3인 공을 선택할 때의 경우의 수 = 2(무게가 3인 공의 개수) * 0(B가 선택하는 경우의 수) = 0
  - 단계가 진행됨에 따라 B가 선택하는 경우의 수 감소
    - 이미 계산했던 경우, 이미 계산했던 조합을 제외하기 때문