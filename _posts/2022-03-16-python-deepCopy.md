---
title: "[Python] deepcopy - 깊은복사 정리"
date: "2022-03-16 18:32:51"
categories: [Python]
tags: [Python]

---

### 객체 복사 개념


- 파이썬에서 변수는 자신에게 대입된 객체를 가리키는 일종의 포인터 같은 존재이다.
- 그러므로 변수 자체는 저장공간을 할당받지 않으며 객체를 가리키는 개념이다.

**Mutable 객체** : 가변 속성
**Immutable 객체** : 불변 속성

```python
a = 1
b = a
print(a, b) # 1 1
b = 2
print(a, b) # 1 2
# int의 자료형은 Immutable하여 a,b 값이 서로 다름

a = [1, 2, 3, 4]
b = a
print(a, b) # [1, 2, 3, 4] [1, 2, 3, 4]
# list 자료형은 Mutable하여 a,b값이 동일하게 변화
```

<img width="622" alt="mutable_immutable" src="https://user-images.githubusercontent.com/74512114/193144600-a123bdd9-c1f4-464b-b112-291f0f47c5b6.PNG">

-----

> 얕은 복사(Shallow Copy)
> - 객체를 새로운 객체로 복사하지만 원본 객체의 주소값을 복사하는것

> 깊은 복사(Deep Copy)
> - 전체 복사로 참조값의 복사가 아닌 참조된 객체 자체를 복사
> - ex) 원본 배열의 보존을 할 필요가 허다하기 때문에 이럴때는 배열을 '깊은 복사' 하여야 한다.

### DeepCopy 예시

```python
# copy모듈 deepcopy() 이용
import copy

a = [1, 2, 3, 4]
b = a
b[1] = 0
print(a, b) # [1, 0, 3, 4] [1, 0, 3, 4]

# !=

a = [1, 2, 3, 4]
b = copy.deepcopy(a)
b[1] = 0
print(a, b) # [1, 2, 3, 4] [1, 0, 3, 4]
```

- deepcopy로 복사된 b는 a값이 아닌 a값이 참조하는 [1,2,3,4] 자체를 참조한다
- b[1] 값을 변경하면 원본 a는 그대로 이고, b값만 바뀌게 된다
<br>

**클래스가 가지고있는 copy() 함수 이용**

```python
a = [1, 2, 3, 4]
b = a.copy()
b[1] = 0
print(a,b) # [1, 2, 3, 4] [1, 0, 3, 4]
```

**list를 생성할 때 매개변수에 원본을 전달,
혹은 생성후 원본 리스트를 확장**

```python
a = [1, 2, 3, 4]
b = list(a)
b[1] = 0
print(a,b) # [1, 2, 3, 4] [1, 0, 3, 4]
```

```python
a = [1, 2, 3, 4]
b = []
b.extend(a)
b[1] = 0
print(a,b) # [1, 2, 3, 4] [1, 0, 3, 4]
```

**리스트 슬라이싱**

```python
a = [1, 2, 3, 4]
b = a[:]
b[1] = 0
print(a,b) # [1, 2, 3, 4] [1, 0, 3, 4]
```

**배열요소를 통한 접근 복사**

```python
a = [1, 2, 3, 4]
b = [i for i in a]
b[1] = 0
print(a,b) # [1, 2, 3, 4] [1, 0, 3, 4]
```

```python
a = [1, 2, 3, 4]
b = []
for i in range(len(a)):
    b.append(a[i])
b[1] = 0
print(a,b) # [1, 2, 3, 4] [1, 0, 3, 4]
```

**※ 주의 :
리스트 슬라이싱이나 제네릭 copy의 copy() 메소드에서 리스트가 오브젝트를 포함할 경우 그 오브젝트들은 얕은복사됨**


**※ 참고 : 처리속도는 리스트 슬라이싱이 가장 빠르고 copy 모듈의 deepcopy() 메소드가 가장 느리다**
