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

**인스턴스 변수란?**
- 인스턴스변수란 각각의 인스턴스 마다 독립한 변수
- 각각의 인스턴스 변수는 다른 것으로 취급하는 변수에 값을 대입해도, 인스턴스마다 각각의 값을 보존

1) 인스턴스 변수의 선언과 접근 방법
