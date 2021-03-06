---
title: "백준 알고리즘 문제 풀이 - 골드바흐의 추측(9020)"
comments: true
categories:
  - Algorithm
tags:
  - 알고리즘 문제 풀이
  - 에라토스테네스의 체
---

## Baekjoon Problem #9020 - 2보다 큰 모든 짝수는 두 소수의 합으로 나타낼 수 있음을 구하는 문제

1보다 큰 자연수 중에서  1과 자기 자신을 제외한 약수가 없는 자연수를 소수라고 한다. 예를 들어, 5는 1과 5를 제외한 약수가 없기 때문에 소수이다. 하지만, 6은 6 = 2 × 3 이기 때문에 소수가 아니다.

골드바흐의 추측은 유명한 정수론의 미해결 문제로, 2보다 큰 모든 짝수는 두 소수의 합으로 나타낼 수 있다는 것이다. 이러한 숫자를 골드바흐 숫자라고 한다. 또, 짝수를 두 소수의 합으로 나타내는 표현을 그 숫자의 골드바흐 파티션이라고 한다. 예를 들면, 4 = 2 + 2, 6 = 3 + 3, 8 = 3 + 5, 10 = 5 + 5, 12 = 5 + 7, 14 = 3 + 11, 14 = 7 + 7이다. 10000보다 작거나 같은 모든 짝수 n에 대한 골드바흐 파티션은 존재한다.

2보다 큰 짝수 n이 주어졌을 때, n의 골드바흐 파티션을 출력하는 프로그램을 작성하시오. 만약 가능한 n의 골드바흐 파티션이 여러 가지인 경우에는 두 소수의 차이가 가장 작은 것을 출력한다.

> 입력
> : 첫째 줄에 테스트 케이스의 개수 T가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고 짝수 n이 주어진다. (4 ≤ n ≤ 10,000)

> 출력
> : 각 테스트 케이스에 대해서 주어진 n의 골드바흐 파티션을 출력한다. 출력하는 소수는 작은 것부터 먼저 출력하며, 공백으로 구분한다.

***
예제 입력 1
```
3
8
10
16
```
예제 출력 1
```
3 5
5 5
5 11
```

***
### My Solution in Python :ok_hand:

```python
m = 10000
s = [0,0] + [1]*(m-1)
for i in range(2, int(m**0.5)+1):
    for j in range(i+i, m+1, i):
        if s[i]: s[j]=0
for _ in range(int(input())):
    n = int(input())
    r = [(x, n-x) for x, y in enumerate(s[:n//2+1]) if y and s[n-x]][-1]
    print(r[0], r[1])
```

> 1번 라인부터 5번 라인까지의 중첩 for 문은 에라토스테네스의 체를 사용하여 10,000까지의 소수를 모두 구하는 코드입니다. 소수에 해당하는 인덱스에는 그 값이 1로 저장되며, 소수가 아니면 0이 저장됩니다.  
> 따라서 이 문제를 해결하는 코드는 실질적으로 8번 라인 단 한 줄이 됩니다.  
> ```python
> r = [(x, n-x) for x, y in enumerate(s[:n//2+1]) if y and s[n-x]][-1]
> ```
>
> 코드의 각 부분을 살펴보면,  
> 우선 8 = 3 + 5나 8 = 5 + 3이나 그 결과는 같기 때문에, 문제에서 작은 소수부터 먼저 출력하라고 했으므로, 우리는 에라토스테네스의 체를 사용하여 구한 소수를 저장해 놓은 리스트 s에서 n//2+1까지만 살펴보면 됩니다.  
> 여기서 enumerate() 함수는 시퀀스형 데이터를 전달받아 그 값을 인덱스와 함께 반환해 줍니다. 즉, 변수 x에는 인덱스가 저장되며, 변수 y에는 해당 인덱스에 저장된 값이 저장되는 것입니다.  
>
> 이때 s[x]의 값이 1이고 동시에 s[n-x]의 값도 1이라면, 정수 n은 두 소수의 합으로 이루어진 골드바흐 파티션이 존재한다고 할 수 있습니다.  
> 만약 이렇게 구한 골드바흐 파티션이 여러 개라면 가장 마지막 요소가 두 소수의 차이가 가장 작은 파티션이므로, -1번째 인덱스를 가지는 요소를 출력하면 됩니다.

***
백준 온라인 저지 [https://www.acmicpc.net/problem/9020](https://www.acmicpc.net/problem/9020)
