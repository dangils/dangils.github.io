---
title: "[Python] Numpy 기본 문법"
date: "2022-03-11 19:21:12"
categories: [Python]
tags: [Python,Numpy]

toc : true
future : true

---

### Numpy
- python에서 벡터,행렬등 수치 연산을 수행하는 선형대수(Linear algebra) 라이브러리
- 내부적으로 C로 구현되었으며 연산이 빠르다.
- N차원 배열(array)객체이며 모든 배열의 값이 기본적으로 같은 타입이어야 한다.

```python

import numpy as np
import numpy.random as np

a = np.arrange(15).reshape(3,5)
print(a)

# [[ 0  1  2  3  4]
#  [ 5  6  7  8  9]
#  [10 11 12 13 14]]

3행 5열의 array
```

#### numpy.ndarray 의 대표적인 속성값

- ndarray.shape : 배열의 각 축(axis)의 크기
- ndarray.ndim : 축의 갯수(Dimension)
- ndarray.dtype : 각 요소(Element)의 타입
- ndarray.itemsize : 각 요소(Element)의 타입의 bytes 크기
- ndarray.size : 전체 요소(Element)의 개수
![](https://images.velog.io/images/hangils/post/a8d0eca9-1902-4f78-b877-c20e02e1389b/image.png)

#### 배열 생성 - array creation

- a = np.array( [2, 3, 4] )
- np.zeros(shape) : 0으로 구성된 N차원 배열 생성
- np.ones(shape) : 1로 구성된 N차원 배열 생성
- np.empty(shape) : 초기화되지 않은 N차원 배열 생성

np.arrange() 와 np.linspace()를 이용하여 연속적인 데이터 생성

- np.arange() : N 만큼 차이나는 숫자 생성
- np.linspace() : N 등분한 숫자 생성

```python
# 10이상 30미만까지 5씩 차이나는 배열 생성
print(np.arrange(10,30,5))
[10 15 20 25]

# 0 ~ 99 까지 100등분
x = np.linspace(0, 99, 100)
print(x)
# [ 0.  1.  2.  3.  4.  5.  6.  7.  8.  9. 10. 11. 12. 13. 14. 15. 16. 17.
#  18. 19. 20. 21. 22. 23. 24. 25. 26. 27. 28. 29. 30. 31. 32. 33. 34. 35.
#  36. 37. 38. 39. 40. 41. 42. 43. 44. 45. 46. 47. 48. 49. 50. 51. 52. 53.
#  54. 55. 56. 57. 58. 59. 60. 61. 62. 63. 64. 65. 66. 67. 68. 69. 70. 71.
#  72. 73. 74. 75. 76. 77. 78. 79. 80. 81. 82. 83. 84. 85. 86. 87. 88. 89.
#  90. 91. 92. 93. 94. 95. 96. 97. 98. 99.]
```
![](https://images.velog.io/images/hangils/post/e49dba71-2a39-4134-8384-391cf4e0b96d/image.png)

배열 출력 - print arrays

3D 배열은 2차원 배열이 N개 출력되는 형식으로 나타남

```python
b = np.arange(12).reshape(4,3)
print(b)
# [[ 0  1  2]
#  [ 3  4  5]
#  [ 6  7  8]
#  [ 9 10 11]]

c = np.arange(24).reshape(2,3,4)
print(c)
# [[[ 0  1  2  3]
#   [ 4  5  6  7]
#   [ 8  9 10 11]]
#
#  [[12 13 14 15]
#   [16 17 18 19]
#   [20 21 22 23]]]

# reshape()을 통해 데이터는 유지한채 차원만 변경가능
# [10000] 배열을 [100, 100] 배열로 변경
np.arange(10000).reshape(100,100)
```
#### Numpy 연산
numpy에서 수치연산은 기본적으로 숫자 각각의 요소에 연산 적용

```python
a = np.array( [20,30,40,50] )
b = np.arange( 4 )
print(b)
# [0 1 2 3]

# a에서 b에 각각의 원소를 -연산
c = a-b
print(c)
# [20 29 38 47]

# b 각각의 원소에 제곱 연산
print(b**2)
# [0 1 4 9]

# a 각각의 원소에 *10 연산
print(10*np.sin(a))
# [ 9.12945251 -9.88031624  7.4511316  -2.62374854]

# a 각각의 원소가 35보다 작은지 Boolean 결과
print(a<35)
# [ True  True False False]
```

2차원 배열을 행렬이라고 볼때, 여러가지 곱셈법

- * : 각각의 원소끼리 곱셈
- @ : 행렬 곱셈
- .dot() : 행렬 내적

-----

#### numpy 내장함수

.sum(): 모든 요소의 합
.min(): 모든 요소 중 최소값
.max(): 모든 요소 중 최대값
.argmax(): 모든 요소 중 최대값의 인덱스
.cumsum(): 모든 요소의 누적합

![](https://images.velog.io/images/hangils/post/c9326243-dd6a-4b1a-87ef-61ed077d8d6d/image.png)

Numpy 차원 변경 함수
![](https://images.velog.io/images/hangils/post/b890fed1-52c1-4c44-9635-d642b3bbca6d/image.png)

-----

#### broadcasting rules
numpy에서 array 연산시 편리성을 위해 shape가 다른 np.array끼리 연산을 지원해주기 위한 기법

```python
np.array([1,2,3,4,5]) * 2
# 결과
# [2,4,6,8,10]

#내부적 수행 과정
# → np.array([1,2,3,4,5]) * np.array([2,2,2,2,2])
```

차원(ndim)이 같고, 각 축(axis)의 값이 같거나 1일 경우 연산이 가능
```python
print(np.arange(4) * 2)
# [0 2 4 6]

print(np.ones((3,4)) * np.arange(4))
# [[0. 1. 2. 3.]
#  [0. 1. 2. 3.]
#  [0. 1. 2. 3.]]

print(np.arange(3).reshape((3,1)) * np.arange(3))
# [[0 0 0]
#  [0 1 2]
#  [0 2 4]]
```
![](https://images.velog.io/images/hangils/post/fe91033b-8d78-4712-846d-e8c631429d61/image.png)

[**Numpy-공식문서**](https://numpy.org/doc/stable/user/basics.broadcasting.html)
