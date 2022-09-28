---
title: "[Python] OOP(Object Oriented Programming) 기본 개요"
date: "2022-03-08 19:11:02"
categories: [Python]
tags: [Python,OOP]


---

### Object Oriented Programming
- class(설계도), object(객체), attribute(변수), method(함수)


```python
# 파이썬에서 모든 attribute, method는 기본적으로 public 즉 클래스 외부에서 attribute, method 접근 가능

# public
class Quadrangle:
    def __init__(self, width, height, color):
        self.width = width
        self.height = height
        self.color = color

    def get_area(self):
        return self.width * self.height

    def set_area(self, width, height):
        self.width = width
        self.height = height

square = Quadrangle(5,5,'blue')
square.width

dir(square)
# 내부 구조에 method가 전부 포함 되어 있음


['__class__',
 '__delattr__',
 '__dict__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__le__',
 '__lt__',
 '__module__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 '__weakref__',
 'color',
 'get_area',
 'height',
 'set_area',
 'width']



 # protected
'''
- python에서 해당 속성의 앞에 _(single underscore) 를 붙여서 표시만 함
- 실제 제약되진 않고 일종의 경고 표시로 사용
'''
class Quadrangle2:
    def __init__(self, width, height, color):
        self.width = width
        self.height = height
        self.color = color

    def _set_area(self, width, height):
        self._width = width
        self._height = height
```

----------------

### Class Inheritance(상속)

- abstraction : 여러 클래스에 중복되는 속성, 메서드를 하나의 기본 클래스로 작성하는 작업
- inheritance : 기본 클래스의 공통 기능을 물려받고, 다른 부분만 추가 또는 변경하는것
- ( 상위 : parent, super, base class / 하위 : child, sub, derived class )


```python

class Figure:
    def __init__(self, name, color) :
        self.__name = name
        self.__color = color

class Quadrangle(Figure):
    def set_area(self, width, height) :
        self.__width = width
        self.__height = height

    def get_info(self):
        print(self.name, self.color, self.__width * self.__height)


square = Quadrangle('square','blue')
square.set_area(5,5)
square.get_info()

'''
double underscore 속성으로 접근이 안되어 error 발생
'''


 class Figure:
    def __init__(self, name, color) :
        self.name = name
        self.color = color

class Quadrangle(Figure):
    def set_area(self, width, height) :
        self.__width = width
        self.__height = height

    def get_info(self):
        print(self.name, self.color, self.__width * self.__height)


square = Quadrangle('square','blue')
square.set_area(5,5)
square.get_info()

-> square blue 25

```

**클래스 변수** : 클래스 정의에서 메서드 밖에 존재 하는 변수
- 해당 클래스를 사용하는 모두에게 공용으로 사용되는 변수
- 클래스 변수는 클래스 내외부에서 '클래스명.변수명' 으로 엑세스 가능

<br>

**인스턴스 변수** : 클래스 정의의 메서드 안에서 사용되면서 "self.변수명" 처럼 사용되는 변수
- 각 객체별로 서로 다른 값을 가짐
- 클래스 내부에서는 self.인스턴스변수명 을 사용하여 엑세스, 클래스 밖에서는 객체명.인스턴스변수명 으로 엑세스


```python
class Figure:
    count = 0  # 클래스 변수

    # 생성자(initializer)
    def __init__(self, width, height):
        # self.* : 인스턴스변수
        self.width = width
        self.height = height

        # 클래스 변수 접근 예
        Figure.count += 1

    def __del__(self):
        Figure.count -= 1


figure2 = Figure(2, 3)
Figure.count

figure1 = Figure(2, 3)
print(Figure.count)
```
**instance method** : 해당 객체 안에서 호출 (지금까지 다룬 self.메서드명을 의미함)
- 해당 메서드를 호출한 객체에만 영향을 미침
- 객체 속성에 접근 가능


**static method** : 객체와 독립적이지만, 로직상 클래스내에 포함되는 메서드
- self 파라미터를 갖고 있지 않음
- 객체 속성에 접근 불가
- 정적 메서드는 메서드 앞에 @staticmethod 라는 Decorator를 넣어야 함
- 클래스명.정적메서드명 or 객체명.정적메서드명 둘 다 호출 가능

```python
class Figure :
    # 생성자
    def __init__(self,width, height):
        self.width = width
        self.height = height

    #메서드
    def calc_area(self):
        return self.width * self.height

    #정적 메서드 (Figure에 너비와 높이가 같은 도형은 정사각형임을 알려주는 기능)
    @staticmethod
    def is_square(rect_width, rect_height):
        if rect_width == rect_height:
            return "정사각형이 될 수 있는 너비/높이"
        else:
            return "될수 없습니다."

figure1 = Figure(2,3)
print(figure1.is_square(5,5))
print(Figure.is_square(3,5))

->
정사각형이 될 수 있는 너비/높이
될수 없습니다.

```


