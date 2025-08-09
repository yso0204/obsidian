# OOP란?
OOP는 **객체 지향 프로그래밍(object-oriented programming)** 의 약자이다.
객체 지향 프로그램밍은 sw를 개발 할 때, **Object** 라는 개념을 중심으로 프로그램을 구성하는 방법론
객체는 데이터와 이 데이터를 처리하는 함수를 하나로 묶은 단위이다.
목표는 코드의 재사용성, 유지 보수성, 확장성을 높이는 것

# 절차 지향 VS 객체 지향
```mermaid
flowchart LR
    subgraph 절차_지향
        D1[데이터1]
        D2[데이터2]
        F1[함수1]
        F2[함수2]
        D1 --> F1
        D2 --> F2
    end

    subgraph 객체_지향
        O1[객체1: 데이터+메서드]
        O2[객체2: 데이터+메서드]
    end
```

| 구분      | 절차 지향 | 객체 지향        |
| ------- | ----- | ------------ |
| 데이터와 동작 | 분리    | 객체에 함께 포함    |
| 코드 구조   | 순서 중심 | 현실 세계 모델링 중심 |
| 재사용성    | 낮음    | 높음           |
| 유지보수    | 어려움   | 쉬움           |
| 확장성     | 불편    | 편리           |
# OOP의 4대 특성
```mermaid
%%{init: {
    'theme': 'default',
    'themeVariables': {
        'fontFamily': 'Nanum Gothic, sans-serif',
        'fontSize': '16px',
        'primaryColor': '#e0f7fa',
        'primaryBorderColor': '#00838f',
        'primaryTextColor': '#006064',
        'lineColor': '#004d40'
    }
}}%%
mindmap
  root((OOP 4대 특성))
    추상화
      설명: 핵심 속성과 동작만 모델링
    캡슐화
      설명: 데이터와 메서드를 묶고, 접근 제한
    상속
      설명: 기존 클래스 기능 재사용 및 확장
    다형성
      설명: 같은 메서드 호출이 객체마다 다르게 동작

```

# 주요 용어
- 클래스(class) : 객체를 만들기 위한 설계도
- 객체(object) : class 에서 생성된 실제 인스턴스
- 속성(attribute) : 객체가 가진 데이터
- 메서드(method) : 객체가 수행하는 동작
- 생성자(Constructor) : 객체 생성 시 초기화 담당 메서드
- 오버라이딩(Overriding) : 상속받은 메서드를 재정의
- 합성(Composition) : 객체가 다른 객체를 속성으로 포함하는 관계("has-a")

# 예시로 이해하는 OOP
## 클래스와 객체
> 클래스는 객체를 만들기 위한 설계도이고, 객체는 그설계도를 기반으로 생성된 실체

```python
class Car :
	def __init__(self,brand,model):
		self.brand = brand
		self.model = model

	def drive(self) :
		print(f"{self.brand} {self.model} is driving")
myCar = Car("Tesla","Model S")
myCar.drive() # Teslas Model S is driving
```

## 상속(Inheritance)
> 기존 클래스를 기반으로 새로운 클래스를 만들고 기능을 추가

```python
class ElectricCar(Car):
    def charge(self):
        print(f"{self.brand} {self.model} is charging!")

my_electric_car = ElectricCar("Tesla", "Model X")
my_electric_car.charge() # Tesla Model X is charging!
```


## 캡슐화(Encapsulation)
> `__brand` 처럼 속성을 private으로 선언해 외부에서 직접 접근을 막고, 메서드를 통해 접근하도록 함

```python
class Car:
    def __init__(self, brand, model):
        self.__brand = brand  # private 속성
        self.model = model

    def get_brand(self):
        return self.__brand

my_car = Car("Tesla", "Model S")
print(my_car.model) # Model S
print(my_car.get_brand()) # Tesla
print(my_car.__brand) # error
```

## 다형성(Polymorphism)
> 같은 메서드(speak)를 호출하지만, 객체 타입에 따라 다른 동작을 수행

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        print("Woof")

class Cat(Animal):
    def speak(self):
        print("Meow")

animals = [Dog(), Cat()]
for animal in animals:
    animal.speak()

Woof
Meow
```

# 절차 지향 -> OOP 예시

## 절차 지향
> 데이터와 함수를 따로 관리하며, 종이 늘어날 수록 함수와 분기문도 함께 늘어나는 방식

```python
dog_name = "바둑이"
cat_name = "나비"

def dog_speak(name):
    print(f"{name}: 멍멍!")

def cat_speak(name):
    print(f"{name}: 야옹!")

dog_speak(dog_name)
cat_speak(cat_name)
```

## 객체 지향
> 동물이라는 공통 클래스를 만들고, 각 동물별 동작을 상속/오버라이딩으로 정의하여 확장성과 유지보수성을 높임

```python
class Animal:
    def __init__(self, name):
        self.name = name
    def speak(self):
        print(f"{self.name}: ...")

class Dog(Animal):
    def speak(self):
        print(f"{self.name}: 멍멍!")

class Cat(Animal):
    def speak(self):
        print(f"{self.name}: 야옹!")

zoo = [Dog('바둑이'),Cat('나비')]

for i in zoo :
    i.speak()

바둑이: 멍멍!
나비: 야옹!
```

# 상속(Inheritance)과 합성(Composition)
## 상속과 합성 비교

| 구분  | 상속                        | 합성                                        |
| --- | ------------------------- | ----------------------------------------- |
| 관계  | “is-a” 관계                 | “has-a” 관계                                |
| 예시  | 개는 동물이다(Dog is an Animal) | 개는 짖는 행동을 가지고 있다(Dog has a Bark behavior) |
| 특징  | 부모-자식 계층 구조               | 객체 안에 다른 객체를 넣음                           |
| 장점  | 코드 재사용이 쉽다                | 유연하게 동작을 교체 가능                            |
| 단점  | 부모 변경 시 자식에 영향 큼(결합도↑)    | 구현이 조금 더 복잡                               |

## 왜 합성이 필요한가?
상속만 쓰다 보면, 아래와 같은 문제가 발생함
- 부모 클래스가 바뀌면 모든 자식 클래스가 영향을 받음(결합도 높음)
- 여러 동작을 조합해야 하면, **다중 상속 문제** 가 생김
- 