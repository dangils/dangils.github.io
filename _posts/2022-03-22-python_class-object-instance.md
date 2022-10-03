---
title: "[Python] Class, Object, Instance 정리"
date: "2022-03-22 21:12:45"
categories: [Python]
tags: [Python]


---

### Class, Object, Instance 개념 정리

> Class
> - 주로 어떤 틀에 비유됨, 즉 같은 무엇을 계속 만들어 내는것
> - 클래스는 객체(Object)를 정의하고 만들기 위한 변수와 메서드의 집합

-  class의 객체(object)가 sw에서 실체화 되면 그것이 instance

```python
class car:
    def on(self):
        print('car!!')

ray = car()
ray.on()
```
1) ray는 객체(object)
2) ray 객체(object)는 car 클래스의 인스턴스(ray = car() 로 실체화 됨)
- 인스턴스(instance)라는 표현은 특정 객체가 어떤 클래스의 객체인지 관계를 중점으로 표현할 때 사용

----

### 인스턴스 변수란?
- 인스턴스변수란 각각의 인스턴스 마다 독립한 변수
- 각각의 인스턴스 변수는 다른 것으로 취급하는 변수에 값을 대입해도, 인스턴스마다 각각의 값을 보존

1) 인스턴스 변수의 선언과 접근 방법
- 일반적으로 인스턴스 변수의 생성은 생성자 클래스 __init__() 내부에서 이루어진다.

```self.인스턴스변수 = 값```

2) 인스턴스 변수의 사용예

```python
class Myclass:

  def __init__(self, text) : # 초기화 : 인스턴스 작성시에 자동적으로 호출된다.
    self.vlaue = text # 인스턴스 변수 value를 선언한다.

  def print_value(self): # 인스턴스 변수 value의 값을 표시하는 함수
    print(self.value) # 인스턴스 변수 value에 접근하고 표시한다.

if __name__ = "__main__":
  a = MyClass("123") # 인스턴스 a를 작성
  b = MyClass("abc") # 인스턴스 b를 작성

  print(a.value) # 123
  print(b.value) # abc

  a.print_value() # 123
  b.print_value() # abc
```
- python에서 클래스 내에 정의된 메소드로부터 인스턴스 변수로 접근하는 경우에 메소드(인스턴스 메소드)의 인수에 self를 전달하여 접근
- 인수 self로는 자동적으로 인스턴스 자체가 전달된다.

------

### 클래스 변수란?
- 클래스 변수는 인스턴스 변수와 달리 모든 인스턴스 사이에 공유된 값을 가진 변수
- 클래스 변수는 인스턴스를 생성하는 것이 아닌 참고하는 것이 가능

1) 클래스 변수의 선언과 접근방법
```python
class MyClass:
    클래스변수 = 값
```
- 클래스 변수 접근 ```클래스.클래스변수```

2) 클래스 변수의 사용예
```python
class MyClass:
	value = "abc" # 클래스 변수를 선언

if __name__ == "__main__":
	print MyClass.value # abc

```
- 클래스의 인스턴스를 생성하는 것이 아닌 MyClass의 클래스 변수 value에 접근하여 값을 표시

> 클래스의 인스턴스를 생성하고 클래스 변수를 표시
```python
class MyClass:
	vlaue = 0 # 클래스 변수를 선언

    def __init__(self): # 초기화 : 인스턴스 생성
    	MyClass.value += 1

if __name__ == "__main__":
	a = MyClass() # 인스턴스 a를 생성한다.
    print MyClass.vlaue # 1

    b = MyClass() # 인스턴스 b를 생성한다.
    print MyClass.value # 2
```

3) 클래스 변수 사용시 주의사항
- 클래스 변수에 접근할 때는 특별히 이유가 없다면 '인스턴스.클래스변수' 나 'self.클래스변수'와 같이 접근하는 것은 피해야한다.
- python에는 인스턴스 변수를 인스턴스 객체로부터 생성하는 것이 가능하므로 의도치 않게 클래스 변수를 인스턴스 변수로 은폐해버리는 경우가 있다.

----

### 클래스 변수 - 인스턴스 변수 차이점
<img width="486" alt="class-instance" src="https://user-images.githubusercontent.com/74512114/193594201-e46b139c-5054-4cec-b6a0-bfab155eab71.PNG">

