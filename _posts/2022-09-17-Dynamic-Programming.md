---

title: "Dynamic Programming"
date: "2022-09-18 21:19:00"
categories: [Algorithm]
tags: [Algorithm, python, DynamicProgramming]

toc : true
future : true

---

### Dynamic Programming

> ### 프로그래밍에서 다이나믹이란?
> - '프로그램이 실행되는 도중에 ' 라는 의미


### 다이나믹 프로그래밍 사용 조건
1) 큰 문제를 작은 문제로 나눌 수 있다.
2) 작은 문제에서 구한 정답은 그것을 포함하는 큰 문제에서도 동일하다.

----

> Memoization(메모이제이션) 기법이란?
> - 다이나믹 프로그래밍을 구현하는 방법 중 하나로, 구한 결과를 메모리
  공간에 저장하고 같은 식을 호출하면 저장한 값을 가져오는 방식
> - 값을 저장하는 방법으로 캐싱(caching)이라고도 한다

<br>

```python
# Memoization을 활용한 피보나치 수열 구현
# Memoization -> 탑다운 방식

# 한 번 계산된 결과를 메모이제이션 하기 위한 리스트 초기화
d = [0] * 100

# 피보나치 함수(Fibonacci Function)를 재귀함수로 구현(탑다운 다이나믹)
def fibo(x):
    # 종료 조건(1 혹은 2일 때 1을 반환)
    if x == 1 or x == 2:
        return 1

    # 이미 계산한적 있는 문제라면 그대로 반환
    if d[x] != 0:
        return d[x]

    # 아직 계산하지 않은 문제라면 점화식에 따라 피보나치 반환
    d[x] = fibo(x-1) + fibo(x-2)
    return d[x]

print(fibo(99))
```

<br>


```python
# 피보나치수열 보텀업 방식

# 앞서 계산된 결과를 저장하기 위한 DP 테이블 초기화
d = [0] * 100

# 첫 번째 피보나치 수와 두 번째 피보나치 저장
d[1] = 1
d[2] = 1
n = 99

# 피보나치 반복문으로 구현(보텀업 다이나믹 프로그래밍)
for i in range(3, n+1):
    d[i] = d[i-1] + d[i-2]

print(d[n])
```

* 보텀업 방식에서 사용되는 결과 저장용 리스트는 'DP 테이블' 이라고 부르며
메모이제이션은 탑다운 방식에 국한되어 사용되는 표현이다.

<br>


















