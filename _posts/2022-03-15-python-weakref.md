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


