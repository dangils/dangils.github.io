---
title: "[Python] weakref 약한참조 사용 및 python 메모리 누수 확인"
date: "2022-03-15 21:40:02"
categories: [Python]
tags: [Python]


---
### weakref 정리

- 파이썬은 Objective-C와 비슷하게 `참조 카운트(Reference Count)`기반의 자동 메모리 관리 모델을 따르고 있다.

- 파이썬의 모든 변수는 값을 담는 영역이 아니라 객체에 바인딩 되는 이름이다.
→ 객체와 이름이 바인딩 되면, 해당 객체는 그 이름에 의해 참조 되고 참조 카운트를 1 증가시킨다.

- 그 이름이 더 이상 해당 객체를 가리키지 않게 되는 경우, (변수 스코프를 벗어나거나 다른 객체에 바인딩 되는 경우) 참조 카운트는 1이 감소
→ 그 결과로 참조 카운트가 0이 되면 객체는 GC 도움 없이 즉시 파괴된다.


> 바인딩이란?
> - 프로그램의 기본단위(ex 변수)에 해당 단위가 가질수 있는 속성을 연결해 주는것
> - python 에서 abc = 10 이라고 하면, abc 변수에 int 10이 바인딩 된것

**참조 카운트 확인**
```python

import sys

class RefExam():
  def __init__(self):
    print('create object')

a = RefExam()
print(f'count {sys.getrefcount(a)}')
b = a
print(f'count {sys.getrefcount(a)}')
c = a
print(f'count {sys.getrefcount(a)}')
c = 0
print(f'count {sys.getrefcount(a)}')
b = 0
print(f'count {sys.getrefcount(a)}')

"""
OUT PUT:
count 2
count 3
count 4
count 3
count 2
"""

# 맨 처음 2가 출력되는 이유는 getrefcount()의 파라미터값으로 임시 참조되기 때문
```
------

객체가 참조수 0이 되거나 다른 이유로 메모리에서 해제될 때에는 해당 객체의 `__del__() [소멸자]` 호출
(특정 클래스에서 이 메소드를 변경해서 객체가 제거되는 시점에 필요한 리소스 정리를 할 수 있다.)


**참조 카운트 0이 될때**
```python

class Foo:
  def __init__(self):
    self.value = 1
  def __del__(self):
    print(f'Object({id(self)}:{self.__class__}) is being destroyed.')

a = Foo() # class Foo 인스턴스 생성

a = 1  # a 변수에 int 1 바인딩 -> Foo() 참조 카운트 -1

# >> Object(1443682546880:<class '__main__.Foo'>) is being destroyed.
```
- Foo클래스를 참조하고 있는 a 변수에 int 1을 바인딩하여 Foo 클래스의 소멸자가 호출된다.

```python
a = Foo()
b = Foo()
a = b  ## 1)

# Object(1087b8192b0:<class '__main__.Foo'>) is being destroyed.

b = 1  ## 2)
a = 2  ## 3)

# Object(1087b827ba8:<class '__main__.Foo'>) is being destroyed.

```
1) a, b 인스턴스 생성, a변수에 b 바인딩 → 맨처음 a에 할당된 Foo()의 소멸자가 호출됨
2) b변수에 int 1 바인딩, 하지만 a는 맨 처음 생성된 b 객체(Foo()가 바인딩된)를 참조 하고있으므로 b에 바인딩 되었던 Foo()는 사라지지 않음

3) a변수에 int 2가 바인딩 되어 a가 참조하던 Foo()의 소멸자가 호출됨

----

### WeakRef 약한 참조

>클래스 인스턴스의 속성이 다른 클래스의 인스턴스를 참조하거나, 동일 클래스의 다른 인스턴스를 참조할 가능성이 높다면 이는 `메모리 누수`가 발생할 가능성이 매우 높은 지점
>  - 약한 참조는 대상 객체를 참조는 하지만 reference count(참조 카운트)를 올리지 않는다.
>  - 약한 참조는 weakref 모듈의 ref 클래스를 통해 생성한다.

**사용 예시**
```python
import weakref
a_set = {0,1}

a_ref = weakref.ref(a_set) # 1)

print(a_ref)
print(a_ref())

a_set = {2, 3, 4} # 2)
print(a_ref()) # 3)
print(a_ref() is None)

# >>>
# <weakref at 0x000001DD6BBEA810; to 'set' at 0x000001DD6BD7D740>
# {0, 1}
# None
# True
```
1) a_ref 변수에 a_set을 할당한다. a_set의 {1,2} 값을 a_ref가 참조
2) a_set 변수에 새로운 값 {2,3,4}를 할당한다. 1)에서의 a_ref가 더이상 {0,1}을 참조하지 않는다.
3) a_ref()는 참조값이 없어져 None을 반환한다.



### 약한 참조를 써야 하는 곳
- 한 개 이상의 객체가 참조 순환 고리를 만드는 경우 메모리 누수를 방지하기 위해 주로 사용
- 용량이 큰 객체를 자주 사용하거나, 쉽게 만들 수 있을 때
- caching에 사용하면 효과적 : 대용량 이미지 데이터를 가지고 있을 때, 메모리 관리를 편하게 하기위해 (local에 제한을 둠)





