---
title: "[Python] Observer Pattern 정리"
date: "2022-04-03 20:11:10"
categories: [Python]
tags: [DesignPattern]


---

### Observer Pattern

- 옵저버 패턴은 하나의 관찰대상, 여러 개의 관찰자 구조가 필요할 때 쓰인다.
- 주체에 종속된 관찰자들에게 주체가 변경됨을 자동을 알리는 디자인 패턴으로,
분산 이벤트 처리 시스템 구현시 사용한다.

![image](https://user-images.githubusercontent.com/74512114/195215572-a63cd85c-3d00-44ea-9160-5355485253ef.png)

> Subject
> - 관찰 대상이 되는 객체
> - 자신을 관찰하는 옵저버 리스트를 가지고 관리도 함 (옵저버 붙이기(attach), 제거(detach), 알리기(notfiy) 를 가짐.)


> Obsever
> - Subject 를 관찰하는 객체
> - Subejct 가 notify 를 호출하면 Observer 의 update 도 호출됨.
> - 즉 observer.update()에 관찰 대상이 notify 했을 때의 할 일들을 작성

------------

### 활용 상황
- 관찰대상 - 관찰자의 구조를 가질 때 사용
- 이벤트 핸들러가 대표적인 옵저버 패턴의 예
  (이벤트 핸들러 : Observer, 이벤트 : Subject)


**구현 예시**

```python
# 관찰 대상
subject = ConcreteSubject()

# 관찰할 옵저버를 만들고, 관찰 대상에 옵저버를 붙인다.
observer_a = ConcreteObserverA()
subject.attach(observer_a)

observer_b = ConcreteObserverB()
subject.attach(observer_b)

# 관찰 대상은 자기 할일 함. 이때 마다 전파!
subject.some_business_logic()

# 관찰 대상에서 옵저버를 뗀다.
subject.detach(observer_a)

class Subject():
    def __init__(self) -> None:
        self._observers = []

    def attach(self, observer: Observer) -> None:
        self._observers.append(observer)

    def detach(self, observer: Observer) -> None:
        self._observers.remove(observer)

    def notify(self) -> None:
        for observer in self._observers:
            observer.update(self)

    def some_business_logic(self) -> None:
        # 어떤 필요한 로직을 진행
        # 이후 자신을 관찰하고 있는 옵저버들에게 알림.
        self.notify()

class Observer(metaClass=ABCMeta):
    @abstractmethod
    def update(self, subject: Subject) -> None:
        pass

class ConcreteObserverA(Observer):
    def update(self, subject: Subject) -> None:
        # 관찰 중인 대상을 파라미터로 받아, 해야하는 일 처리.

class ConcreteObserverB(Observer):
    def update(self, subject: Subject) -> None:
        # 관찰 중인 대상을 파라미터로 받아, 해야하는 일 처리.
```



### 참고

https://wikidocs.net/83755
