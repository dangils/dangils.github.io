---
title: "Design Patterns 개요"
date: "2022-08-02 19:20:00"
categories: [CS,Design Patterns]
tags: [CS, Python, Design Patterns]

toc : true
future : true

---



## SOLID 원칙
객체지향 설계 원칙
<br>

1) Single Responsibility Principle
- 하나의 클래스는 하나의 역할만을 수행
<br>

2) Open - close Principle
- 확장(상속)에는 열려있고, 수정에는 닫혀 있어야 함
<br>

3) Liskov Substitution Principle
- 자식이 부모의 자리에 항상 교체될 수 있어야 한다
- 부모의 property / method 모두를 자식이 가지고 있어야 함
<br>

4) Interface Segregation Principle
- 인터페이스가 잘 분리되어 클래스가 꼭 필요한 인터페이스만 구현이 되어있음
<br>

5) Dependency Inversion Property
- 상위 모듈이 하위 모둘에 의존하면 안됨
- 메타 클래스 / 추상화 클래스에 의존(필요하면), 추상화 자체는 세부 사항에 의존하면 안됨

<br>

## Design Pattern
잘 설계된 구조의 형식적 정의. 다양한 디자인 패턴으로 서로 다른 문제를 해결 가능

<br>

#### 디자인 패턴이 필요한 이유
- 중복되는 코드 개발을 하고 싶지 않을 때 "바퀴를 다시 발명하지 마라"
- 업무의 분리를 위해, 개념을 압축해 효율적인 커뮤니케이션 가능
- 유지보수 용이 / 객체지향 기술 향상 -> OOP 기술의 문제점에 대한 해결책 제시

<br>

![image](https://user-images.githubusercontent.com/74512114/147792109-dfc936a4-095a-4db1-82d4-bd42f919d79d.png)

<br>

#### 디자인 패턴의 구조
- 맥락(context) :
문제가 발생하는 여러 상황을 기술한다. 즉, 패턴이 적용될 수 있는 상황을 나타낸다. 경우에 따라서는 패턴이 유용하지 못한 상황을 나타내기도 한다.

<br>

- 문제(problem) :
패턴이 적용되어 해결될 필요가 있는 여러 디자인 이슈들을 기술한다. 이때, 여러 제약 사항과 영향력도 문제 해결을 위해 고려해야 한다.

<br>

- 해결(solution) :
문제를 해결하도록 설계를 구성하는 요소들과 그 요소들 사이의 관계, 책임, 협력 관계를 기술한다.
해결은 반드시 구체적인 구현 방법이나 언어에 의존적이지 않으며 다양한 상황에 적용할 수 있는 일종의 템플릿이다.


[파이썬 OOP 개념 및 디자인패턴 자료 참고](https://www.fun-coding.org/PL&OOP2-2.html)




--------


## 주요 GOF 디자인 패턴

<br>

### 1) Adapter Pattern
용도
- 어떤 클래스를 바로 사용할 수 없을때. 다른곳에서 개발한 클래스이고, 이를 수절할 수 없을 떄, 중간에 변환할 역할을 해주는 클래스가 필요한데 이것이 바로 어댑터

<br>

사용방법
- 상속
- 위임 : 어떤 메소드의 실제 처리를 다른 인스턴스의 메소드에게 맡기는 방법

<br>

Class Diagram
![image](https://user-images.githubusercontent.com/74512114/147891171-6b58af6b-9d04-4d60-aebb-7f5ae6a02e98.png)


<br>

### 2) Prototype Pattern
용도
- 미리 만들어진 객체를 복사해서 객체를 생성하는 방식
- 객체를 많이 만들어야 할 경우, 객체 생성에 드는 코딩 분량을 현저히 줄일 수 있다
- 클래스로부터 객체를 생성하기 어려운 경우(그래픽 에디터에서 사용자의 마우스 클릭으로 생성되는 객체들)

<br>

사용 방법
- 모형(Prototype) 인스턴스를 등록해 놓고, 등록된 인스턴스를 복사(clone())해서 인스턴스를 생성함

![image](https://user-images.githubusercontent.com/74512114/147891187-f69b2806-cd1c-471b-81a5-54bce36b572e.png)

<br>

### 3) Singleton Pattern
용도
- 시스템 내부에 1개의 인스턴스만 생성하고 싶은 경우
- 컴퓨터 자체를 표현한 클래스, 현재 시스템 설정을 표현한 클래스

<br>

사용방법
- 생성자를 private으로 선언하고, 해당하는 생성자를 클래스 내부에서만 호출함

![image](https://user-images.githubusercontent.com/74512114/147891197-2fc72591-9e49-4bff-80c0-d36790b5a78d.png)

<br>

### 4) Composite Pattern
용도
- 틀과 내용물을 같은 것으로 취급하고 싶을 때(디렉토리 내부에는 디렉토리와 파일이 있지만, 둘 모두 디렉토리 내부에 있는 Element로 표현하고 싶을 때)

<br>

사용 방법
- Composite 클래스가 Component를 포함하도록 함
![image](https://user-images.githubusercontent.com/74512114/147891217-c094005a-79b7-419b-b9fa-fdf8ba3cedbf.png)

<br>

### 5) Decorator Pattern
용도
- 데코레이팅한 결과물을 다시 내용물로 보고 그것을 다시 데코레이팅하기 위함(지속적으로 장식을 추가할 때, 문자열 주위에 여러 유형의 border 장식을 추가할 때)

<br>

사용 방법
- 데코레이터(decorator) 패턴은 @ 표기를 사용해 함수 또는 메서드의 변환을 지정해주는 도구이다. 데커레이터 패턴은 함수의 객체와 함수를 변경하는 다른 객체의 래핑 (wrapping) 을 혀용한다. 즉 클래스 내의 메서드를 재정의 하지 않고도 자동으로 다른 함수와 래핑 시켜준다.

![image](https://user-images.githubusercontent.com/74512114/147891227-7c5fc285-779f-4477-8f1b-0b405c0af115.png)

✔ Decorator가 Component를 포함하고 있음

   ```python
class C(object):
    @my_decorator
    def method(self):
        #메서드...
'''
이는 아래와 같은 코드이다.
'''

class C(object:
    def method(self):
        #메서드...
    method = my_decorator(method)
# ================ Decorator 예제 ====================

import random
import time

def benchmark(func):

    def wrapper(*args, **kwargs):  # *args(튜플형태 가변인자) , **kwargs(딕셔너리형태 가변인자)
        t = time.perf_counter()  # 코드 수행시간
        res = func(*args, **kwargs)  # 들어오는 매개변수는 가변길이의 랜덤 리스트
        print(f'{func.__name__} {time.perf_counter()-t}')
        return res

    return wrapper

@benchmark
## random_tree = benchmark(random_tree)
def random_tree(n):
    temp = [n for n in range(n)]
    for i in range(n+1):
        temp[random.choice(temp)] = random.choice(temp)  # 랜덤 리스트 생성
    #temp = n
    return temp

random_tree(1000)
# -> random_tree 0.0005249

# @classmethod , @staticmethod
'''
이들은 각각 메서드를 클래스 메서드와 정적 메서드로 변환한다. @classmethod는 첫 번째 인수로 클래스(cls)를 사용하고,
@staticmethod는 첫 번째 인수에 self 혹은 cls가 없다. 클래스 내 변수에 접근하려면 @classmethod의 첫 번째 인수를 사용할 수 있다.
'''
class A(object):
_hello = True

    def foo(self, x):
        print(f'{self} // {x}')

    @classmethod
    def class_foo(cls,x): # 클래스 내 변수에 접근하려면 @classmethod의 첫 번째 인수로 접근
        print(f'class_foo({cls} , {x}) 실행 : {cls._hello}')

    @staticmethod
    def static_foo(x):
        print(f'static_foo({x})')

a = A()
a.foo(1)
a.class_foo(2)
A.class_foo(2)
a.static_foo(3)
A.static_foo(3)

# foo(<__main__.A object at 0x03CDA400>, 1) 실행
# class_foo(<class '__main__.A'>, 2) 실행: True
# class_foo(<class '__main__.A'>, 2) 실행: True
# static_foo(3) 실행
# static_foo(3) 실행

   ```


<br>

### 6) Facade Pattern
용도
- 대규모 프로그램에는 서로 관련있는 클래스들이 많음 -> 복잡하게 얽혀있는 클래스들을 정리해서 높은 레벨의 인터페이스(API)를 제공(간단하게 접근 가능)
- 여러 클래스들을 직접 제어하지 않고 '창구(facade)'에 요구함
- 결과적으로 구현시에 간단한 인터페이스를 사용할 수 있게함

![image](https://user-images.githubusercontent.com/74512114/147891238-4101be0d-0df4-4336-b417-372d0dcc6d4a.png)

<br>

### 7) Proxy Pattern
용도
- proxy(대리인) -> 시간이 많이 걸리는 작업은 대리인이 수행
- 시간이 많이 걸리는 작업을 할 때, 대리인이 할 수 있는 일은 대리인이 하고 할 수 없는 일(Heavy job)은 본래의 클래스에게 넘겨줌
>ex) 시스템 초기화는 필요하지 않은 기능까지 초기화하려고 하면 많은 시간이 필요한데, 그 기능을 Proxy에 위임함
프린트 프로그램에서 실제 프린터를 실행하는 과정에 시간이 오래 걸리기 때문에 그 과정에 있는 일들을 Proxy에 위임함

<br>

사용 방법
- proxy 클래스에 우선 일을 위임하고, 그 뒤에 RealSubject가 해야할 일은 넘겨주는 방법으로 사용
![image](https://user-images.githubusercontent.com/74512114/147891244-0da4d5b5-3d93-4156-a9ac-07535cbd787e.png)

<br>

### 8) Observer Pattern
용도
> 특정 값을 유지하는 핵심 객체를 갖고, 직렬화된 객체의 복사본을 생성하는 일부 옵저버(관찰자)가 있는 경우 유용하다.
즉, 객체의 일대다(one-to-many) 의존 관계에서 한 객체의 상태가 변경되면, 그 객체에 종속된 모든 객체에 그 내용을 통지하여 자동으로 상태를 갱신하는 방식이다.
(마치 provider 또는 subscriber) 옵저버 패턴은 @property 데커레이터를 사용해 구현할 수 있다.
예를 들어 속성 (property)을 읽기 전용으로 설정하는 것과 같은 속성 접근 제어를 할 수 있다. 속성은 접근자 (accessor), getter/setter 메서드 대신 사용된다.

- 관찰 대상의 상태가 변화했을 때 관찰자에게 통지하는 패턴
- 상태 변화에 따른 처리를 기술할 때 효과적으로 활용 (MVC패턴에서 model과 view의 분리 등)
- 이벤트 핸들러 : Observer , 이벤트 : Subject / observer 객체들은 subject에 의존성을 갖는다.
- subject 객체를 관찰하여 변경을 감지하고자 하는 객체를 observer로 등록하고 변경이 되었을 때, 이를 탐지
ex) a라는 유튜브 채널(subject)을 A,B,C 라는 사람이 구독을 하게 되면(observer) 해당 채널에 새로운 영상이나 글이 올라올 경우(객체의 상태 변경), 해당 유튜브를 구독한 A,B,C는 알림을 받게 된다. -> 1(subject) : N(observer) 구조

<br>

사용 방법
- Observer 클래스에 상태 변화를 알려주고, Observer는 다시 그 변화에 맞는 결과를 나타냄
![image](https://user-images.githubusercontent.com/74512114/147891246-000430f7-24d0-4182-b687-9233f70236d2.png)


<br>

```python

# 옵저버 패턴 구현 예제

class Subscriber(object):
    def __init__(self, name):
        self.name = name
    def update(self, message):
        print(f'{self.name} , {message}')

class Publisher(object):
    def __init__(self):
        self.subscribers = set()
    def register(self, who):
        self.subscribers.add(who)
    def unregister(self, who):
        self.subscribers.discard(who)
    def dispatch(self, message):
        for subsciber in self.subscribers:
            subsciber.update(message)

pub = Publisher()

beom = Subscriber('Beom')
ben = Subscriber('Ben')
seok = Subscriber('Seok')

pub.register(beom)
pub.register(ben)
pub.register(seok)

pub.dispatch("lunch")
pub.unregister(ben)
pub.dispatch("dinner")

```






