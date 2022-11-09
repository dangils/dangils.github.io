---
title: "[Python] List Comprehension, 정렬 기본 문법 정리"
date: "2022-03-01 15:14:00"
categories: [Python]
tags: [Python, List Comprehension]

toc : true
future : true

---


### Python List Comprehension

> 리스트를 초기화 하는 방법중 하나로 대괄호 안에([]) 조건문과 반복문을 넣는 방식으로 리스트를 초기화

```python
array = [i for i in range(21) if i%2==0]

array= [i*i for i in range(1,9) if i%2==0]

print(array)

﻿[4, 16, 36, 64]
```

- N*M 크기의 2차원 리스트 초기화

```python
n=3
m=4
array=[[0]*m for _ in range(n)] #﻿ 단순 반복시 i를 _로 대체 가능'
print(array)
```
* 2차원 리스트를 초기화 할때는 반드시 리스트 컴프리헨션을 이용. 다음과 같이 초기화 할 시 의도하지 않은 결과가 나올 수 있다.

```python
array =[[0]*m]*n
print(array)

array[1][1]=5
print(array)

[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
[[0, 5, 0, 0], [0, 5, 0, 0], [0, 5, 0, 0]]
```
- 이는 내부적으로 포함된 3개의 리스트가 모두 동일한 객체에 대한 3개의 래퍼런스로 인식되기 때문

<br>

------

- python 정렬 기본 문법

```python
a=[1,4,3]
print('기본리스트 : ',a)

#리스트에 원소 삽입
a.append(2)
print("삽입 : ",a)

#오름차순 정렬
a.sort()
print("오름차순 정렬: ",a)

#내림차순 정렬
a.sort(reverse=True)
print("내림차순 정렬 : ",a)

#리스트 원소 뒤집기
a.reverse()
print("원소 뒤집기 : ",a)

# 특정 인덱스에 데이터 추가 (해당 자리에 넣고 다른것 뒤로 밀어냄)
a.insert(2,3)
print("인덱스 2에 3추가 ",a)

#특정 값인 데이터 개수 세기

print("값이 3인 데이터 개수 : ", a.count(3))

a.remove(1)

print("값이 1인 데이터 삭제 : ",a)

기본리스트 :  [1, 4, 3]
삽입 :  [1, 4, 3, 2]
오름차순 정렬:  [1, 2, 3, 4]
내림차순 정렬 :  [4, 3, 2, 1]
원소 뒤집기 :  [1, 2, 3, 4]
인덱스 2에 3추가  [1, 2, 3, 3, 4]
값이 3인 데이터 개수 :  2
값이 1인 데이터 삭제 :  [2, 3, 3, 4]

#insert 함수는 원소 삽입후 위치를 조정하므로 append 함수보다 동작이 느리다.
```

- 특정한 원소값 제거

```python
a= [1,2,3,4,5,5,5]
remove_set = {3,5}

#remove_set에 포함되지 않은 값만을 저장
result = [i for i in a if i not in remove_set]

print(result)

[1, 2, 4]
```

----

### Tuple
- 튜플은 한 번 선언된 값을 변경할 수 없다.
- 리스트는 대괄호[], 튜플은 소괄호()
- 튜플 자료형은 그래프 알고리즘을 구현시 자주 사용
- ex) 다익스트라 최단 경로 알고리즘, 알고리즘 → 우선순위 큐에 한 번 들어간 값은 변경되지 않는다.


### Dictionary
- 키(key)와 값(Value)의 쌍을 데이터로 가지는 자료형

```python
data= dict()
data['사과']= "Apple"
data['바나나']='Banana'
data['코코넛']= 'coconut'

print(data)

if '사과' in data:
    print("'사과'를 키로 가지는 데이터가 존재합니다.")

{'사과': 'Apple', '바나나': 'Banana', '코코넛': 'coconut'}
'사과'를 키로 가지는 데이터가 존재합니다.
```

### Set
- 집합(set)을 처리하기 위한 자료형
- 중복을 혀용하지 않음
- 순서가 없다. → 사전 자료형과 집합 자료형은 순서가 없으므로 인덱싱으로 값을 얻을 수 없다.

```python
#집합 자료형 초기화 방법 - 1

data = set([1,1,2,3,4,4,5])
print(data)

#집합 자료형 초기화 방법 - 2
data = {1,1,2,3,4,4,5}
print(data)

{1, 2, 3, 4, 5}
{1, 2, 3, 4, 5}

# 집합 자료형 연산, 관련 함수

#합집합 : | , 교집합 : & , 차집합 : -

# 집합 자료형 관련 함수 : remove(),updata()

data={1,2,3}
print(data)

#새로운 원소 추가
data.add(4)
print(data)

#새로운 원소 여러 개 추가
data.update([5,6])
print(data)

#특정한 값을 갖는 원소 삭제
data.remove(3)
print(data)

{1, 2, 3}
{1, 2, 3, 4}
{1, 2, 3, 4, 5, 6}
{1, 2, 4, 5, 6}
```
