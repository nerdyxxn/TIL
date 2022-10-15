# 객체지향 프로그래밍(Object Oriented Programming)

> OOP(Object Oriented Programming)란 '객체지향 프로그래밍' 이라고 하며 컴퓨터 프로그래밍 디자인의 철학(또는 패러다임) 중 하나

<br>

## 💡 객체지향 프로그래밍(Object Oriented Programming)이란?

> OOP에서는 객체를 중심으로 프로그래밍이 이루어지며, 사람이 세계를 보고 이해하는 방법을 흉내낸 방법론

- OOP는 구성으로는 Class와 Object(Class의 인스턴스), Method가 있음
  1. Class: 자동차 생산을 위한 청사진
  2. Object: 청사진의 속성과 기능을 담아 만들어진 생산물
  3. Method: 자동차가 가지는 전진, 후진, 정지와 같은 기능들

<br>
<br>

## 💡 객체지향 프로그래밍(Object Oriented Programming)의 특징

**1. 캡슐화**

- 데이터 구조와 데이터를 다루는 방법을 결합시켜 묶는 것
  객체 내에 관련된 내용과 그 내용의 메소드를 하나로 묶어 캡슐처럼 묶음
  <br>

**2. 상속화**

- 상위 클래스의 특징을 하위 클래스에서 물려 받을 수 있음
  부모와 자식의 관계처럼 부모의 특징을 가지고 자식에세 물려줌
  <br>

**3. 추상화**

- 객체들의 공통적인 특징(속성, 기능)을 추출하는 것(클래스를 정의하는 과정)
  전화기는 크게 수화기와 버튼으로 나뉘지만, 이를 위해 내부는 복잡하게 구성된 것이 하나의 예시
  <br>

**4. 다형성**

- 상위 클래스로부터 같은 상속을 받더라도 각각의 하위 클래스의 기능이 다를 수 있음 (한 부모 밑에서 낳은 자식이라도 모두 같지 않은 것처럼)
  HTMLElement와 각 태그의 render()의 관계

<br>
<br>

## 💡 JavaScript에서 Object를 생성하는 여러가지 방법들

> Class는 하나의 정형화된 모델을 만들어 두고, 그 모델을 기반으로 한 인스턴스(Object)을 만들기 위해 사용됨

<br>

#### 2.1. Functional instantiation

- 함수를 이용해서 찍어내는 방식

```jsx
var Car = function () {
  var someInstance = {};
  someInstance.position = 0;
  someInstance.move = function () {
    this.position += 1;
  };
  return someInstance;
};

var car1 = Car();
var car2 = Car();
car1.move();
```

<br>

#### 2.2. Functional Shared instantiation

- 메소드, 클래스 그리고 이들을 합치는 함수를 따로 만드는 방식
- 메소드를 클래스로 부터 분리하여 모든 인스턴스들이 클래스 내에 있는 모든 메소드들을 할당받는 것을 방지(메모리 효율 상승)

```jsx
var extend = function (to, from) {
  for (var key in from) {
    to[key] = from[key];
  }
};

var someMethods = {};
someMethods.move = function () {
  this.position += 1;
};

var Car = function (position) {
  var someInstance = {
    position: position,
  };
  extend(someInstance, someMethods);
  return someInstance;
};

var car1 = Car(5);
var car2 = Car(10);
```

<br>

#### 2.3. Prototypal instantiation

- Functional Shared instantiation 방식과 유사하지만 Object.create() 함수를 사용함

```jsx
var someMethods = {};
someMethods.move = function () {
  this.position += 1;
};

var Car = function (position) {
  var someInstance = Object.create(someMethods);
  someInstance.position = position;
  return someInstance;
};

var car1 = Car(5);
var car2 = Car(10);
```

<br>

#### 2.4. Pseudoclassical instantiation

- 메소드를 프로토타입으로 만들며, new operator를 붙여야 함

```jsx
var Car = function (position) {
  this.position = position;
};

Car.prototype.move = function () {
  this.position += 1;
};

var car1 = new Car(5);
var car2 = new Car(10);
```

<br>
<br>
