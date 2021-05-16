---
title: javascript 19Prototype
date: 2020-09-29 22:17:59
category: "javascript"
draft: false
---

# 프로토타입

**자바스크립트의 패러다임**

자바스크립트는 명령형(imperative), 함수형(functional), 프로토타입기반(prototype-based) 객체지향 프로그래밍(OOP;Object Oriented Programming)을 지원하는 멀티 패러다임 프로그래밍 언어다.

**다른 객체지향 언어와의 자이**

C++이나 JAVA 같은 클래스 기반 객체지향 프로그래밍 언어의 특징인 클래스와 상속, 캡슐화를 위한 키워드인 public, private, protected 등이 없어서 자바스크립트는 객체지향 언어가 아니라고 오해를 받ㄱ는 경우도 있다. 하지만 자바스크립트는 클래스 기반 객체지향 프로그래밍 언어보다 효율적이며 더 강력한 객체 지향 프로그래밍 능력을 지니고 있는 프로토타입 기반의 객체지향 프로그래밍 언어다.

**자바스크립트의 클래스(class)**

ES6에서 클래스가 도입되었다. 하지만 ES6의 클래스가 기존의 프로토타입 기반 객체지향 모델을 퍠지하고 새로운 객체지향 모델을 제공하는 것은 아니다.

사실 클래스도 함수이며, 기존 프로토타입 기반 패턴의 문법적 설탕(syntactic sugar)이라고 볼 수 있다.

클래스와 생성자 함수는 모두 프로토타입 기반의 인스턴스를 생성하지만 정확히 동일하게 동작하지는 않는다. 클래스는 생성자 함수보다 엄격하며 클래스는 생성자 함수에서는 제공하지 않는 기능도 제공한다.

따라서 클래스를 프로토타입 기반 객체 생성 패턴의 단순한 문법적 설탕으로 보기보다는 새로운 객체 생성 메커니즘으로 보는것이 더 합당하다.

**자바스크립트는 핵심 : 객체**

자바스크립트는 객체 기반의 프로그래밍 언어이며 자바스크립트를 이루고 있는 거의 모든것이 객체다. 원시타입(primitive type)의 값을 제외한 나머지 값들 (함수, 배열, 정규표현식 등)은 모두 객체다.

## 1. 객체 지향 프로그래밍

**객체지향 프로그래밍이란**

객체지향 프로그래밍(Object Oriented Programming, OOP)은 프로그램을 명령어 또는 함수의 목록으로 보는 전통적인 명령형 프로그래밍(imperativie programming)의 절차지향적 관점에서 벗어나 여러 개의 독립적 단위인 객체(object)의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임을 말한다.

**객체의 의미**

객체지향 프로그래밍은 실세계의 실체(사물이나 개념)룰 인식하는 철학적 사고를 프로그래밍에 접목하려는 시도에서 시작한다. 실체는 특징이나 성질을 나타내는 속성(attribut/ property)를 가지고 있고, 이를 통해 실체를 인식하거나 구별할 수 있따.

예를들어, 사람은 다음과 같은 속성을 갖는다.

- 이름
- 주소
- 성별
- 나이
- 신장
- 학력
- 직업
- 등등

위의 속성들에 대응되는 구체적인 값을 넣어주면, 예를들어 "이름이 정지만, 나이는 23세, 성별은 남자인 사람"과 같이 속성을 구체적으로 표현하면 특정사람을 다른사람과 구별하여 인식할 수 있다.

이러한 방식을 프로그래밍에 접목시킨것이 객체지향 프로그래밍이다.

객체지향 프로그래밍 시 우리는 객체의 필요한 속성, 일부 속성만 추려내어 객체를 표현한다. 이를 추상화라고 한다.

**추상화 예시 **

사람을 구현하려고 한다. 사람에게는 위에서 기술한 것과 같이 수많은 속성을 가지고 있다. 하지만 우리가 구현하려는 프로그램은 사람의 이름과 나이만 관심을 가지고 있다고 가정한다. 이처럼 여러 속성 중에서 프로그램에 필요한 속성만 간추려내어 표현하는 것을 추상화(abstraction)이라고 한다.

```
const person = {
	name: 'jiman',
	age: 23
};
```

**객체 지향 프로그래밍과 객체**

프로그래머는 객체(object)를 다루는 주체(subject)라고 할 수 있다. 우리는 위 예제에서 만든 person 객체의 속성인 이름과 나이를 보고 다른 객체와 구별하여 인식할 수 있다.

즉 객체는 속성을 통해 열 개의 값을 하나의 단위로 구성한 복합적인 자료구조를 말한다. 객체지향 프로그래밍은 독립적인 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임이다.

**객체의 상태(state)와 동작(behavior)**

원(Circle)이라는 개념을 객체로 만들어보자. 원에는 반지름이라는 속성이 있다. 이 반지름을 가지고 원의 지름, 둘레, 넓이를 구할 수 있다. 이때 반지름은 원의 상태를 나타내는 데이터이며, 원의 지름, 둘레, 넓이를 구하는 것은 동작이다.

```
const Circle = {
	radius: 5,

	getDiameter() {
		return 2 * this.radius;
	}

	getPerimeter() {
		return 2 * this.radius * Math.PI;
	}

	getArea() {
		return Math.PI * this.radius ** 2;
	}
 };
```

위 예제와 같이 객체지향 프로그래밍은 객체의 상태(state)를 나타내는 데이터와 상태 데이터를 조작할 수 있는 동작(behavior)을 하나의 논리적인 단위로 묶어 생각한다

객체는 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조라고 할 수 있다. 객체의 상태 데이터를 property, 동작을 method라고 한다.

**객체의 관계성(relationship)**

각 객체는 고유의 기능을 갖는 독립적인 부품으로 볼 수 있지만 자신의 고유한 기능을 수행하면서 다른 객체와 관계성(relationship)을 가질 수 있다. 다른 객체와 메시지를 주고 받거나 데이터를 처리할 수도 있다. 또는 다른 객체의 상태 데이터나 동작을 상속받아 사용하기도 한다.

## 2. 상속과 프로토타입

**상속이란**

상속(inheritance)은 객체지향프로그래밍의 핵심 개념으로, 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할 수 있는 것을 말한다.

**상속의 역할**

자바스크립트는 프로토타입을 기반으로 상속을 구현하여 불필요한 중복을 제거한다. 중복을 제거하는 방법은 기존의 코드를 적극적으로 재사용하는 것이다. 코드 재사용은 개발 비용을 현저히 줄일 수 있는 잠재력이 있으므로 매우 중요하다.

```
//생성자 함수
function Circle(radius) {
	this.radius = radius;

	this.getDiameter = function() {
		return 2 * this.radius;
	};

	this.getPerimeter = function() {
		return 2 * Math.PI * this.radius;
	};

	this.getArea = function() {
		return Math.PI * this.radius ** 2;
	};
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);
```

위 예제와 같이 생성자 함수는 동일한 프로퍼티 구조를 갖는 객체를 여러개 생성할 때 유용하다.

**위 예제 생성자 함수의 문제점**

Circle 생성자 함수가 생성하는 모든 객체(instance)는 radius 프로퍼티와 메서드들을 갖는다. radius 프로퍼티값은 보통 인스턴스마다 다르다. 하지만 getDiameter, getPerimeter, getArea 메서드는 모든 인스턴스들이 동일한 내용의 메서드를 사용하므로 단 하나만 생성하여 모든 인스턴스가 공유해서 사용하는 것이 바람직하다.

하지만, 위 예제의 Circle 생성자 함수의 경우 인스턴스를 생성할 때마다 메서드들을 중복 생성하고 모든 인스턴스가 중복해서 소유한다.

즉, 동일한 생성자 함수에 의해 생성된 모든 인스턴스가 동일한 메서드를 중복 소유하는 것은 메모리를 불필요하게 낭비한다. 또한 인스턴스를 생성할 때마다 메서드를 생성하므로 퍼포먼스에도 악영향을 준다.

즉 공간적, 시간적으로 손해가 생긴다.

**상속을 통한 중복 제거**

상속을 통해 위 예제의 Circle의 불필요한 중복을 제거해본다. 자바스크립트는 프로토타입(prototype)을 기반으로 상속을 구현한다.

```
function Circle(radius) {
	this.radius = radius;
}
// 중복 제거하고자 하는 프로퍼티 메서드는 프로토타입에 추가
Circle.prototype.getDiameter = function() {
	return 2 * this.radius;
}
 Circle.prototype.getPerimeter = function() {
	return Math.PI * 2 * this.radius;
}
Circle.prototype.getArea = function() {
	return Math.PI * this.radius ** 2;
}

//인스턴스 생성
const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1.getArea === circle2.getArea); //true
```

**프로토타입 기반 상속의 원리**

Circle 생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입, 즉 상위 객체 역할을 하는 Circle.prototype의 모든 프로퍼티와 메서드를 상속받는다.

메서드들은 단 한번만 생성되어 프로토타입인 Circle.prototype의 메서드로 할당되어 있다. 따라서 Circle 생성자 함수가 생성하는 모든 인스턴스는 해당 메서드들을 상속받아 사용할 수 있다. 즉, 자신의 상태를 나타내는 radius 프로퍼티만 개별적으로 소유하고 내용이 동일한 메서드는 상속을 통해 공유하여 사용하는 것이다.

**상속의 장점**

상속은 코드의 재사용이란 관점에서 매우 유용하다. 생성자 함수가 생성할 모든 인스턴스가 공통적으로 사용할 프로퍼티나 메서드를 프로토타입에 미리 구현해 두면 생성자 함수가 생성할 모든 인스턴스는 별도의 구현없이 상위(부모)객체인 프로토타입의 자산을 공유하여 사용할 수 있다.

## 3. 프로토타입 객체

**프로토타입 객체란**

프로토타입 객체란 객체지향 프로그래밍의 근간을 이루는 객체 간 상속(inheritance)을 구현하기 위해 사용된다. 프로토타입은 어떤 객체의 상위(부모) 객체의 역할을 하는 객체로서 다른 객체에 공유 프로퍼티(메서드 포함)를 제공한다. 프로토타입을 상속받은 하위 객체는 상위 객체의 프로퍼티를 자신의 프로퍼티처럼 자유롭게 사용할 수 있다.

**프로토타입 내부슬롯 [[Prototype]]**

모든 객체는 [[Prototype]]이라는 내부 슬롯을 가지며, 이 내부 슬롯의 값은 프로토타입의 참조([[Prototype]]의 값이 null 인 경우도 있다.)다. [[Prototype]]에 저장되는 프로토타입은 **객체 생성 방식**에 의해 결정된다. 즉 객체가 생성될 때 객체 생성 방식에 따라 프로토타입이 결정되고 [[Prototype]]에 저장된다.

**객체 생성방식에 따른 prototype 객체**

예시로, 객체 리터럴에 의해 생성된 객체의 프로토타입은 Object.prototype 이고 생성자 함수에 의해 생성된 객체의 프로토타입은 생성자 함수의 prototype 프로퍼티에 바인딩되어 있는 객체다.

**생성자 함수와 프로토타입**

모든 객체는 하나의 프로토타입을 갖는다.([[Prototype]]값이 null 인 객체는 프로토타입이 없다.) 그리고 모든 프로토타입은 생성자 함수와 연결되어 있다.

- 생성자 함수의 prototype 프로퍼티는 생성자 함수의 prototype을 가리킨다.
- 생성자 함수.prototype의 constructor 프로퍼티는 생성자 함수를 가리킨다.
- 생성자 함수가 생성한 인스턴스는 포로토타입의 프로퍼티를 상속받는다
- 생성자 함수에서 `__proto__`접근자 프로퍼티로 프로토타입에 간접적으로 접근할 수 있다.

[[Prototype]] 내부슬롯에 직접 접근할 수 없지만, 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]]내부슬롯이 가리키는 프로토타입에 간접적으로 접근 가능하다.

프로토타입은 자신의 constructor 프로퍼티를 통해 생성자 함수에 접근할 수 있고, 생성자 함수는 자신의 prototype 프로퍼티를 통해 프로토타입에 접근할 수 있다.

### 3.1 `__proto__`접근자 프로퍼티

**`__proto__`접근자 프로퍼티의 기능**

모든 객체는 `__proto__`접근자 프로퍼티를 통해 자신의 프로토타입인 [[Prototype]]내부슬롯에 간접적으로 접근할 수 있다.

```
const student = {
	name: 'jiman';
};
student.__proto;
```

일반 객체에 `__proto__`접근자 프로퍼티를 사용하면 [[Prototype]]내부 슬롯이 가리키는 객체인 Object.prototype에 접근할 수 있다.

모든 객체는 이 접근자 프로퍼티를 통해 프로토타입을 가리키는 [[Prototype]] 내부슬롯에 접근할 수 있다.

**`__proto__`는 접근자 프로퍼티다**

**[[Prototype]] 내부슬롯으로의 접근**

내부슬롯은 프로퍼티가 아니다. 자바스크립트는 원칙적으로 내부슬롯과 내부 메서드에 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않는다.

단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공한다. [[Prototype]] 내부 슬롯에도 직접 접근할 수 없으며 `__proto__`접근자 프로퍼티를 통해 간접적으로 [[Prototype]] 내부슬롯의 값, 즉 프로토타입에 접근할 수 있다.

**접근자 프로퍼티의 특징**

접근자 프로퍼티는 자체적으로 값([[Value]]프로퍼티 어트리뷰트)을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수(accessor function), 즉 [[Get]], [[Set]] 프로퍼티 어트리뷰트로 구성된 프로퍼티다.

**`__proto__`접근자 프로퍼티의 이용**

Object.prototype의 접근자 프로퍼티인 `__proto__` getter / setter 함수라고 부르는 접근자 함수를 통해 [[Prototype]] 내부 슬롯의 값, 즉 프로토타입을 취득하거나 할당한다.

- `__proto__`에 접근시
  - getter 함수 [[Get]]이 호출
- `__proto__`에 할당시
  - setter 함수 [[Set]]이 호출

```
const obj = {};
const parentObj = {x: 1};

console.log(obj.__proto__); // object.prototype
obj.__proto__ = parentObj;
console.log(obj.__proto__); //{ x: 1 }

console.log(obj.x); // 1
```

**`__proto__`접근자 프로퍼티는 상속을 통해 사용된다. **

`__proto__`접근자 프로퍼티는 객체가 직접 소유하는 프로퍼티가 아니라 Object.prototype의 프로퍼티다. 모든 객체는 상속을 통해 Object.prototype.`__proto__`접근자 프로퍼티를 사용할 수 있다.

```
const person = { name: 'Lee'};

console.log(person.hasOwnProperty('__proto__')); //false

console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
//{get: f, set: f, enumerable: false, configurable: false}

console.log({}.__proto__ === Object.prototype);
//true
```

**Object.prototype**

모든 객체는 프로토타입의 계층 구조인 프로토타입 체인에 묶여 있다. 자바스크립트 엔진은 객체의 프로퍼티에 접근하려고 할때 해당 객체에 접근하려는 프로퍼티가 없다면 `__proto__` 접근자 프로퍼티가 가리키는 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다. 프로토타입 체인의 종점, 즉 프로토타입 체인의 최상위 객체는 Object.prototype이며, 이 객체의 프로퍼티와 메서드는 모든 객체에게 상속된다.

**`__proto__`접근자 프로퍼티를 통해 프로토타입에 접근하는 이유**

[[Prototype]] 내부 슬롯의 값, 즉 프로토타입에 접근하기 위해 접근자 프로퍼티를 사용하는 이유는 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서다. `__proto__` 접근자 프로퍼티는 상호 참조가 발생하면 에러를 발생시킨다.

```
const parent = {};
const child = {};

//상호 참조 시 에러
child.__proto__ = parent;
parent,__proto__ = child; // TypeError: Cyclic __proto__ value
```

만약 위 예제 코드가 에러없이 진행되어 각 객체가 서로의 프로토 타입이 된다면 객체 서로가 자신의 프로토타입이 되는 비정상적인 프로토타입 체인이 만들어 진다. `__proto__` 접근자 프로퍼티는 이 경우 에러를 발생시키도록 구현되어 있다.

**프로토타입 체인의 요구조건**

포로토타입 체인은 단방향 링크드 리스트로 구현되어야 한다. 즉, 프로퍼티 검색 방향이 하위에서 상위로, 한쪽 방향으로만 흘러가야한다. 종점에는 Object.prototype이 존재하는 구조로 이루어지게 되는데 서로가 자신의 프로토타입이 되는 순환 참조(circular reference) 구조가 만들어지게되면 종점이 존재하지 않게 된다. 종점이 존재하지 않는다면 존재하지 않는 프로퍼티를 검색할 때 무한 루프에 빠지게 된다.

이러한 상황이 발생하지 않도록 `__proto__` 접근자 프로퍼티가 구현되어 있다.

**`__proto__`접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않는다.**

- 모든 객체가 `__proto__`접근자 프로퍼티를 상속받지는 않는다.

`__proto__` 접근자 프로퍼티는 ES5 까지 ECMAScript 사양에 포함되지 않은 비표준이었다. 하지만 일부 브라우저에서 `__proto__`를 지원하고 있었기 때문에 브라우저 호환성을 고려하여 ES6에서는 표준으로 채택되었다. 그래서 대부분 브라우저가 해당 접근자 프로퍼티를 지원한다.

하지만 모든 객체가 `__proto__` 접근자 프로퍼티를 사용할 수 있는 것이 아니다.

직접 상속을 통해 Object.prototype을 상속받지 않는 객체를 생성할 수도 있다.

```
const obj = Object.create(null);

console.log(obj.__proto__); //undefined

console.log(Object.getPrototypeOf(obj)); //null
```

**getPrototypeOf / setPrototypeOf**

`__proto__`접근자 프로퍼티 대신 프로토타입에 접근하고 싶은 경우 다음과 같은 방법을 사용한다.

- 프로토타입의 참조를 취득
  - Object.getPrototypeOf 메서드 사용
- 프로토타입을 교체
  - Object.setPrototypeOf 메서드 사용

```
const child = {};
const parent = { x: 1 };

Object.getPrototypeOf(child); // child.__proto__와 동일

Object.setPrototypeOf(child, parent); //child.__proto__ = parent; 와 동일

Object.setPrototypeOf(parent, child);
// 순환 참조 시 에러
```

### 3.2 함수 객체의 prototype 프로퍼티

**함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다.**

일반 객체의 경우 [[Prototype]] 내부슬롯은 존재하였지만 prototype 프로퍼티를 직접 소유하고 있지 않았다. 하지만 함수 객체는 prototype 프로퍼티를 소유한다.

```
(function(){}).hasOwnProperty('prototype')// true

({}).hasOwnProperty('prototype') // false
```

prototype 프로퍼티는 생성자 함수가 생성할 객체의 프로토타입을 가리킨다. 따라서 생성자 함수로서 호출할 수 없는 non-constructor인 함수는 prototype 프로퍼티를 소유하지 않고, 프로토타입도 생성하지 않는다.

단 [[Prototype]] 내부 슬롯은 모든 객체가 가지고 있으므로 내부 슬롯은 존재한다.

non-constructor

- 화살표 함수
- 메서드 축약표현으로 정의된 메서드

```
const Person = name => {
	this.name = name;
};

console.log(Person.hasOwnProperty('prototype')); //false

console.log(Person.prototype)// undefined

//메서드 축약 표현
const obj = {
	foo() {}
};

console.log(obj.foo.hasOwnProperty('prototype'));//false

console.log((function(){}).prototype); //{}
console.log(obj.foo.prototype); //undefined
```

생성자 함수로 호출하기 위해 정의하지 않은 일반 함수(함수 선언문, 함수 표현식)도 prototype 프로퍼티를 소유하고 있다. 하지만 객체를 생성할 목적으로 만들어지지 않은 일반함수의 prototype 프로퍼티는 아무 의미가 없다.

**`__proto__` 접근자 프로퍼티 vs 함수의 prototype 프로퍼티**

모든 객체가 가지고 있는 (Object.prototype으로부터 상속받은) `__proto__`접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킨다.

하지만 사용 주체와 목적이 다르다.

| 구분                        | 소유        | 값                | 사용 주체   | 사용 목적                                                          |
| --------------------------- | ----------- | ----------------- | ----------- | ------------------------------------------------------------------ |
| `__proto__` 접근자 프로퍼티 | 모든 객체   | 프로토타입의 참조 | 모든 객체   | 객체가 자신의 프로토타입에 접근 또는 교체하기위해 사용             |
| prototype 프로퍼티          | constructor | 프로토타입의 참조 | 생성자 함수 | 생성자 함수가 자신이 생성할 객체의 프로토타입을 할당하기 위해 사용 |

```
function Person(name) {
	this.name = name;
}

const me = new Person('Lee');

console.log(Person.prototype === me.__proto__) //true
```

### 3.3 프로토타입의 constructor 프로퍼티와 생성자 함수

**모든 프로토타입은 constructor 프로퍼티를 갖는다**

constructor 프로퍼티는 prototype프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킨다. 이 연결은 생성자 함수가 생성될때, 즉 함수 객체가 생성될 때 이루어진다.

```
function Person(name) {
	this.name = name;
}

const you = new Person('Kim');

console.log(you.constructor === Person); //true
```

Person 생성자 함수는 you 객체를 생성하였다. 이때 you 객체는 프로토타입의 constructor 프로퍼티를 통해 생성자 함수와 연결된다. you객체에는 constructor 프로퍼티가 없지만 프로토타입으로부터 상속받아 you 객체도 constructor 프로퍼티를 사용할 수 있다.

## 4, 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

**생성자 함수로 생성한 객체**

생성자 함수에 의해 생성된 인스턴스는 프로토타입의 constructor 프로퍼티에 의해 생성자 함수와 연결된다. constructor 프로퍼티가 가리키는 생성자 함수는 인스턴스를 생성한 생성자 함수이다.

**리터럴로 생성한 객체**

명시적으로 new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하지 않고, 리터럴 표기법에 의한 객체 생성방식과 같은 객체 생성방식도 있다.

```
const obj = {};

const foo = function(){};

const arr = [1, 2, 3];

const regexp = /is/ig;
```

**리터럴로 생성한 객체의 생성자 함수**

모든 객체는 프로토타입 내부슬롯이 있으므로 리터럴 표기법에 의해 생성된 객체도 프로토타입이 존재한다. 하지만 리터럴 표기법에 의해 생성된 객체의 경우 프로토타입의 constructor 프로퍼티가 가리키는 생성자 함수가 반드시 객체를 생성한 생성자 함수라고 단정할 수 없다.

```
const obj = {};

constole.log(obj.constructor === Object); //true
```

위 예제의 obj 객체는 Object 생성자 함수로 생성한 객체가 아니라 객체 리터럴에 의해 생성된 객체다. 하지만 obj 객체는 Object 생성자 함수와 constructor 프로퍼티로 연결되어 있다. 그렇다면 객체 리터럴에 의해 생성된 객체는 사실 Object 생성자 함수로 생성되는 것은 아닐지 하는 의문이 들 수 있다.

**Object 생성자 함수의 ECMAScript 사양**

Object 생성자 함수는 다음과 같이 구현되도록 정의되어 있다.

1. new.target 이 undefined나 Object가 아닌 경우 인스턴스 -> 인스턴스 생성자함수의 프로토타입 - > Object.prototype 순으로 프로토타입 체인이 생성된다.
2. Object. 생성자 함수에 인수를 전달하지 않거나 undefined 또는 null을 인수로 전달하면서 new 연산자와 함께 호출하면 내부적으로는 추상연산 OrdinaryObjectCreate를 호출하여 Object.prototype을 프로토타입으로 갖는 빈 객체를 생성한다.

**추상 연산(abstract operation)**

추상 연산은 ECMAScript 사양에서 내부 동작의 구현 알고리즘을 표현한 것이다. ECMAScript 사양에서 설명을 위해 사용되는 함수와 유사한 의사코드이다.

```
//2. Object 생성자 함수에 의한 객체 생성
// Object 생성자 함수는 new 연산자와 함께 호출하지 않아도 new 연산자와 함께 호출한 것과 동일하게 동작한다.
//인수가 전달되지 않았을 때 추상연산 OrdinaryObjectCreate를 호출하여 빈 객체를 생성한다.

let obj = new Object();
console.log(obj); //{}

//1. new.target이 undefined 나 Object 가 아닌 경우
//인스턴스 -> Foo.prototype&nbsp; -> Object.prototype 순으로 프로토타입 체인이 생성된다.
class Foo extends Object {}
new Foo(); // Foo&nbsp;{}

// 3. 인수가 전달된 경우에는 인수를 객체로 변환한다.
//Number 객체 생성
obj = new Object(123);
console.log(obj); //Number {123}

//String 객체 생성
obj = new Object('123');
console.log(obj);// String{'123'}

```

**객체 리터럴이 평가될때의 추상연산**

객체 리터럴이 평가될 때는 추상연산 OrdinaryObjectCreate를 호출하여 빈 객체를 생성하고 프로퍼티를 추가하도록 정의되어 있다.

Object 생성자 함수 호출과 객체 리터럴의 평가는 추상 연산 OrdinaryObjectCreate를 호출하여 빈 객체를 생성하는 점에서 동일하다.하지만 new.target의 확인이나 프로퍼티를 추가하는 처리 등 세부 내용이 다르다.

따라서 객체 리터럴에 의해 생성된 객체는 Object 생성자 함수가 생성한 함수가 아니다.

**함수 리터럴과 함수 생성자함수**

함수 객체의 경우 차이가 더 명확하다. Function 생성자 함수를 호출하여 생성한 함수는 렉시컬 스코프를 만들지 않고 전역 함수인 것처럼 스코프를 생성하며 클로저도 만들지 않는다. 따라서 함수 선언문과 함수 표현식을 평가하여 함수 객체를 생성한 것은 Function 생성자 함수가 아니다. 하지만 constructor 프로퍼티를 통해 확인해보면 foo 함수의 생성자 함수는 Function 생성자 함수다

```
function foo(){}
console.log(foo.constructor === Function); //true
```

**리터럴로 생성된 객체의 생성자 함수**

리터럴 표기법에 의해 생성된 객체도 상속을 위해 프로토타입이 필요하다. 따라서 리터럴 표기법에 의해 생성된 객체도 가상적인 생성자 함수를 갖는다. 프로토타입은 생성자 함수와 더불어 생성되며 prototype, constructor 프로퍼티에 의해 연결되어 있기 때문이다. 다시 말해, 프로토타입과 생성자 함수는 단독으로 존재할 수 없고 언제나 쌍(pair)으로 존재한다.

리터럴 표기법(객체 리터럴, 함수 리터럴, 배열 리터럴, 정규 표현식 리터럴 등) 에 의해 생성된 객체는 생성자 함수에 의해 생성된 객체는 아니다. 하지만 큰 틀에서 생각해보면 리터럴 표기법으로 생성한 객체도 생성자 함수로 생성한 객체와 본질적인 면에서 큰 차이는 없다.

예를 들어, 객체 리터럴에 의해 생성한 객체와 Object 생성자 함수에 의해 생성한 객체는 생성과정에서 미묘한 차이는 있지만 결국 객체로서 동일한 특성을 갖는다. 함수 리터럴에 의해 생성한 함수와 Function 생성자 함수에 의해 생성한 함수는 생성 과정과 스코프, 클로저 등의 차이가 있지만 결국 함수로서 동일한 특성을 갖는다.

**리터럴로 생성한 객체의 생성자함수 취급**

프로토타입의 constructor 프로퍼티를 통해 연결되어 있는 생성자 함수를 리터럴 표기법으로 생성한 객체를 생성한 생성자 함수로 생각해도 크게 무리는 없다. 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입은 다음과 같다.

| 리터럴 표기법      | 생성자 함수 | 프로토타입         |
| ------------------ | ----------- | ------------------ |
| 객체 리터럴        | Object      | Object.prototype   |
| 함수 리터럴        | Function    | Function.prototype |
| 배열 리터럴        | Array       | Array.prototype    |
| 정규 표현식 리터럴 | RegExp      | RegExp.prototype   |

## 5. 프로토타입의 생성 시점

**프로토타입은 생성자 함수가 생성되는 시점에 생성된다**

리터럴 표기법에 의해 생성된 객체도 생성자 함수와 연결되는 것을 보았다. 객체는 리터럴 표기법 또는 생성자 함수에 의해 생성되므로 결국 모든 객체는 생성자 함수와 연결되어 있다.

(Object.create 메서드와 클래스로 객체를 생성하는 방법도 있다.)

프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성된다. 프로토타입과 생성자 함수는 단독으로 존재할 수 없고 언제나 쌍으로 존재하기 때문이다.

**셍상지 힘수의 구분**

생성자 함수는 정의 주체에 따라 두가지로 구분할 수 있다.

- 사용자 정의 생성자 함수
  - 사용자가 직접 정의한 생성자 함수
- 빌트인 생성자 함수
  - 자바스크립트가 기본 제공하는 생성자 함수

두 생성자 함수의 프로토타입 생성시점에 대해 알아본다.

### 5.1 사용자 정의 생성자 함수와 프로토타입 생성시점

**함수 정의가 평가되는 시점에 생성된다.**

내부 메서드 [[Construct]]를 갖는 함수 객체, 즉 화살표 함수나 ES6의 메서드 축약 표현으로 정의하지 않고 일반함수로 정의한 함수 객체는 new 연산자와 함께 생성자 함수로 호출할 수 있다.

생성자 함수로서 호출할 수 있는 함수, 즉 constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.

```
console.log(Person.prototype); // {}

function Person(){}
```

non - constructor 는 프로토타입이 생성되지 않는다

```
const Person = name => {
	this.name = name;
}

console.log(Person.prototype); // undefined
```

**함수 선언문이 평가되는 시점**

함수 선언문은 다른 코드가 실행되기 이전에 자바스크립트 엔진에 의해 먼저 실행된다. 따라서 함수 선언문으로 정의된 Person 생성자 함수는 어떤 코드보다 먼저 평가되어 함수 객체가 된다.

이때 프로토타입도 더불어 생성된다. 생성된 프로토타입은 Person 생성자 함수의 prototype 프로퍼티에 바인딩된다.

함수선언문에 의한 생성자 함수에 연결된 프로토타입 객체의 프로퍼티

- constructor: 생성자 함수의 참조
- `__proto__` : Object (상속받은 프로퍼티)

**생성된 프로토타입의 프로퍼티**

생성된 프로토타입은 오직 constructor 프로퍼티만을 갖는 객체다. 프로토타입도 객체이고 모든 객체는 프로토타입을 가지므로 프로토타입도 자신의 프로토타입을 갖는다. 생성된 프로토타입의 프로토타입은 Object.prototype이다.

### 5.2 빌트인 생성자 함수와 프로토타입 생성 시점

**빌트인 생성자 함수가 생성되는 시점**

Object, String, Number, Function, Array, RegExp, Date, Promis 등과 같은 빌트인 생성자 함수도 일반 함수와 마찬가지로 빌트인 생성자 함수가 생성되는 시점에 프로토타입이 생성된다. 모든 빌트인 생성자 함수는 전역 객체가 생성되는 시점에 생성된다. 생성된 프로토타입은 빌트인 생성자 함수의 prototype 프로퍼티에 바인딩된다.

**전역 객체(global object)란**

전역 객체는코드가 실행되기이전 단계에 자바스크립트 엔진에의해 생성되는 특수한 객체이다. 전역 객체는 클라이언트 사이드 환경(브라우저)에서는window, 서버 사이드 환경(Node.js)에서는 global 객체를 의미한다.

전역 객체는표준 빌트인 객체(Object, String, Number, Function, Array 등) 들과 환경에 따른 호스트 객체(클라이언트 web API 또는Node.js의 호스트 API), 그리고 var 키워드로 선언한 전역 변수와 전역 함수를 프로퍼티로 갖는다. Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 생성자 함수이다.

**객체가 생성되기 이전에 생성자 함수와 프로토타입은 이미 존재한다.**

표준 빌트인 객체인 Object도 전역객체의 프로퍼티이며, 전역 객체가 생성되는 시점에 생성된다.

이처럼 객체가 생성되기 이전에 생성자 함수와 프로토타입은 이미 객체화되어 존재한다. 이후 생성자 함수 또는 리터럴 표기법으로 객체를 생성하면 프로토타입은 생성된 객체의 [[Prototype]] 내부 슬롯에 할당된다. 생성된 객체는 프로토타입을 상속받는다.

## 6. 객체 생성 방식과 프로토타입의 결정

**객체의 생성방법**

- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스

**공통점**

이처럼 다양한 방식으로 생성된 모든 객체는 각 방식마다 세부적인 객체 생성방식의 차이는 있으나 추상 연산 OrdinaryObjectCreate에 의해 생성된다는 공통점이 있다.

**추상 연산 OrdinaryObjectCreate **

추상 연산 OrdinaryObjectCreate는 필수적으로 자신이 생성할 객체의 프로토타입을 인수로 전달받는다.

그리고 자신이 생성할 객체에 추가할 프로퍼티 목록을 옵션으로 전달할 수 있다. 추상 연산 OrdinaryObjectCreate는 빈 객체를 생성한 후, 객체에 추가할 프로퍼티 목록이 인수로 전달된 경우 프로퍼티를 객체에 추가한다.

그리고 인수로 전달받은 프로토타입을 자신이 생성한 객체의 [[Prototype]] 내부슬롯에 할당하고, 생성한 객체를 반환한다.

즉, 프로토타입은 추상 연산 OrdinaryObjectCreate에 전달되는 인수에 의해 결정된다. 이 인수는 객체가 생성되는 시점에 객체 생성방식에 의해 결정된다.

### 6.1 객체 리터럴에 의해 생성된 객체의 프로토타입

**객체리터럴에 의한 프로토타입 연결**

자바스크립트 엔진은 객체 리터럴을 평가하여 객체를 생성할 때, 추상 연산 OrdinaryObjectCreate를 호출한다. 이때 추상 연산 OrdinaryObjectCreate에 전달되는 프로토타입은 Object.prototype이다. 즉, 객체리터럴에 의해 생성되는 객체의 프로토타입은 Object.prototype 이다.

```
const obj = {x: 1};
```

위 객체 리터럴이 평가되면 추상연산 OrdinaryObjectCreate에 의해 Object 생성자 함수와 Object.prototype과 생성된 객체 사이에 연결이 만들어 진다.

**Object.prototype을 상속받는다**

객체리터럴에 의해 생성된 obj 객체는 Object.prototype을 프로토타입으로 갖게 되며, 이로써 Object.prototype을 상속받는다. obj 객체는 constructor 프로퍼티와 hasOwnProperty 메서드 등을 소유하지 않지만 자신의 프로토타입인 Object.prototype의 constructor 프로퍼티와 hasOwnProperty 메서드를 자신의 자산인 것처럼 자유롭게 사용할 수 있다. 이는 obj 객체가 자신의 프로토타입인 Object.prototype 객체를 상속받았기 때문이다.

### 6.2 Object 생성자 함수에 의해 생성된 객체의 프로토타입

**Object생성자 함수로 생성한 객체의 프로토타입 연결**

Object 생성자 함수를 인수 없이 호출하면 빈 객체가 생성된다. Object 생성자 함수를 호출하면 객체 리터럴과 마찬가지로 추상연산 OrdinaryObjectCreate가 호출된다. 인수로 전달되는 프로토타입은 Object.prototype이다. 객체리터럴과 마찬가지로, Object 생성자 함수에 의해 생성되는 객체의 프로토타입은 Object.prototype 이다.

```
const obj = new Object();
obj.x = 1;
```

**생성된 객체는 객체리터럴에 의해 생성된 객체와 동일한 구조를 갖는다.**

Object 생성자 함수로 생성된 객체 역시 추상 연산 OrdinaryObjectCreate 에 의해 인스턴스와 Object.prototype 간에 상속관계가 만들어진다.

Object.prototype을 프로토타입으로 가진 인스턴스는 프로토타입의 프로퍼티를 상속받아 사용할 수 있다.

**리터럴과 생성자 함수의 생성방식의 차이**

객체 리터럴과 Object 생성자 함수에 의한 객체 생성방식의 차이는 프로퍼티를 추가하는 방식에 있다. 객체 리터럴 방식은 객체 리터럴 내부에 프로퍼티를 추가하지만 Object 생성자 함수 방식은 일단 빈 객체를 생성한 이후 프로퍼티를 추가해야한다.

### 6.3 생성자 함수에 의해 생성된 객체의 프로토타입

**생성자 함수로 생성한 객체의 프로토타입 연결**

new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하면 다른 객체 생성 방식과 마찬가지로 추상 연산 OrdinaryObjectCreate가 호출된다. 이때 추상 연산 OrdinaryObjectCreate에 전달되는 프로토타입은 생성자 함수의 prototype 프로퍼티에 바인딩되어 있는 객체다. 즉, 생성자 함수에 의해 생성되는 객체의 프로토타입은 생성자 함수의 prototype프로퍼티에 바인딩되어 있는 객체이다.

```
function Student(age) {
	this.age = age;
}
const me = new Student(23);
```

위 코드가 실행되면

- 추상연산 OrdinaryObjectCreate 호출
- 인스턴스 다음 객체를 프로토타입으로 연결함
  - 생성자 함수의 prototype 프로퍼티에 바인딩 된 객체

**Object 생성자 함수와 사용자 정의 생성자 함수의 차이**

표준 빌트인 객체인 Object 생성자 함수와 더불어 생성된 프로토타입 Object.prototype 은 다양한 빌트인 메서드를 갖고 있다. 하지만 사용자 정의 생성자 함수 Student와 더불어 생성된 프로토타입 Student.prototype의 프로퍼티는 constructor 뿐이다.

**프로토타입 객체에 프로퍼티 추가**

프로토타입 Student.prototype에 프로퍼티를 추가하여 하위 객체가 상속받을 수 있도록 구현해본다. 프로토타입은 객체이므로 프로퍼티를 추가 삭제하여 프로토타입 체인에 반영시킬 수 있다.

```
function Student(age){
	this.age = age;
}

Student.prototype.showInfo = function(){
	console.log(this.age + '세 입니다');
};

const me = new Student(23);

me.showInfo();//23세 입니다
```

Student 생성자 함수를 통해 생성된 모든 객체는 Student.prototype에 추가된 프로퍼티를 상속받아 사용할 수 있다.

## 7.프로토타입 체인

**사용자 정의 생성자 함수에 의해 생성된 객체의 상속 관계**

```
function Student(age){
	this.age = age;
}

Student.prototype.showInfo = function(){
	console.log(this.age + '세 입니다');
};

const me = new Student(23);
console.log(me.hasOwnProperty('age'));//true
```

Student 생성자 함수에 의해 생성된 me 객체는 Object.prototype 메서드인 hasOwnProperty를 호출할 수 있따. 이것은 me 객체가 Person.prototype 뿐만 아니라 Object.prototype 도 상속받았다는 것을 의미한다.

**프로토타입의 프로토타입은 항상 Object.prototype 이다.**

me 객체의 프로토타입은 Student.prototype 이다.

```
Object.getPrototypeOf(me) === Student.prototype ; // true
```

Student.prototype의 프로토타입은 Object.prototype이다. 프로토타입의 프로토타입은 항상 Object.prototype이다.

```
Object.getPrototypeOf(Studnet.prototype) === Object.prototype; // true
```

Student 생성자 함수로 생성한 객체의 프로토타입 체인 구조는 다음과 같다.

- Student 생성자 함수
  - Function.prototype
    - Object.prototype
- me 인스턴스
  - Student.prototype
    - Object.prototype

**프로토타입의 이용**

자바스크립트는 객체의 프로퍼티에 접근하려고 할 때 해당 객체에 프로퍼티가 없다면 [[Prototype]] 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다. 이를 프로토타입 체인이라고 한다. 프로토타입 체인은 자바스크립트가 객체지향 프로그래밍의 상속을 구현하는 메커니즘이다.

```
me.hasOwnProperty('age'); //true
```

hasOwnProperty는 Object.prototype의 메서드이다. me 객체부터 Student.prototype , Object.prototype 순으로 프로토타입 체인을 거슬러 올라가며 프로퍼티를 검색한다.

**프로토타입 체인의 검색 과정**

me.hasOwnProperty('age') 메서드를 호출하는 과정

1. hasOwnProperty 메서드를 호출한 me 객체에서 해당 메서드를 검색한다. me 객체에는 hasOwnProperty 메서드가 없다. 프로토타입 체인을 따라, [[Prototype]]내부슬롯 에 바인딩된 프로토타입으로 이동한다. Student.prototype에서 해당 메서드를 검색한다.
2. Student.prototype에도 hasOwnProperty 메서드가 없으므로 프로토타입 체인을 따라 [[Prototype]]내부슬롯에 바인딩된 Object.prototype으로 이동하여 해당 메서드를 검색한다.
3. Object.prototype에는 hasOwnProperty 메서드가 존재한다. 자바스크립트 엔진은 Object.prototype.hasOwnProperty 메서드를 호출한다. 이때 해당 메서드의 this 에는 me 객체가 바인딩된다.

**call 메서드에 의한 간접 호출**

```
Object.prototype.hasOwnProperty.call(me, 'age');
```

**call 메서드**

call 메서드는 this로 사용할 객체를 전달하면서 함수를 호출한다. 위 코드에서는 this로 사용할 me 객체를 전달하면서 Object.prototype.hasOwnProperty 메서드를 호출하였다.

**프로토타입의 종점**

프로토타입 체인의 최상위에 위치하는 객체는 언제나 Object.prototype이다. 따라서 모든 객체는 Object.prototype을 상속받는다. Object.prototype을 프로토타입 체인의 종점 (end of prototype chain)이라 한다. Object.prototype 의 프로토타입 즉 [[Prototype]] 내부 슬롯의 값은 null 이다.

- 프로토타입 체인의 종점인 Object.prototype 에서도 프로퍼티를 검색할 수 없는 경우, undefined 를 반환한다. 이때 에러가 발생하지 않는다.

```
console.log(me.hello); //undefined
```

**프로토타입 체인의 의의**

자바스크립트 엔진은 프로토타입 체인을 따라 프로퍼티 / 메서드를 검색한다. 즉, 자바스크립트 엔진은 객체 간의 상속 관계로 이루어진 프로토타입의 계층적인 구조에서 객체의 프로퍼티를 검색한다. 따라서 프로토타입 체인은 상속과 프로퍼티 검색을 위한 메커니즘이라고 할 수 있다.

**스코프 체인과의 차이**

프로토타입 체인이 프로퍼티 검색을 위한 메커니즘이라면, 프로퍼티가 아닌 식별자는 스코프 체인에서 검색한다. 즉, 자바스크립트 엔진은 함수의 중첩관계로 이루어진 스코프의 계층적 구조에서 식별자를 검색한다. 스코프 체인은 식별자 검색을 위한 메커니즘이라고 할 수 있다.

**메서드 호출시 동작 과정**

```
me.hasOwnProperty('age');
```

위 코드를 실행하게 되면 다음과 같은 순서로 동작한다.

1. 스코프 체인에서 me 식별자를 검색한다. me 스코프는 전역에서 선언되었으므로 전역 스코프에서 검색된다.
2. me 객체의 프로토타입 체인에서 hasOwnProperty 메서드를 검색한다.

스코프 체인과 프로토타입 체인은 서로 연관없이 별도로 동작하는 것이 아니라 서로 협력하여 식별자와 프로퍼티를 검색하는 데 사용된다.

## 8. 오버라이딩과 프로퍼티 섀도잉

```
const Student = (function () {
	function Student(age) {
		this.age = age;
	}

	Student.prototype.showInfo = function(){
		console.log(this.age + '세 입니다');
	};

	return Student;
}());

const me = new Student(23);

me.showInfo = function() {
	console.log('안녕하세요 ' + this.age + '세 입니다' );
};

me.showInfo(); // 안녕하세요 23세 입니다
```

**상속 관계에 따른 프로퍼티 숨김**

프로토타입이 소유한 프로퍼티를 프로토타입 프로퍼티, 인스턴스가 소유한 프로퍼티를 인스턴스 프로퍼티라고 부른다.

프로토타입 프로퍼티와 같은 이름의 프로퍼티를 인스턴스에 추가하면 프로토타입 체인을 따라 프로토타입 프로퍼티를 검색하여 프로토타입 프로퍼티를 덮어쓰는 것이 아니라 인스턴스 프로퍼티로 추가한다. 이때 인스턴스 메서드 showInfo는 프로토타입 메서드 showInfo를 오버라이딩했다. 그리고 프로토타입 메서드 showInfo는 가려진다. 이처럼 상속 관계에 의해 프로퍼티가 가려지는 현상을 프로퍼티 섀도잉(property shadowing)이라 한다.

**오버라이딩(overrding)**

상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의하여 사용하는 방식이다.

**오버로딩(overloading)**

함수의 이름은 동일하지만 매개변수의 타입 또는 개수가 다른 메서드를 구현하고 매개변수에 의해 메서드를 구별하여 호출하는 방식이다. 자바스크립트는 오버로딩을 지원하지 않지만 arguments 객체를 사용하여 구현할 수는 있다.

**프로퍼티를 삭제하는 경우**

```
delete me.showInfo;

me.showInfo(); //23세 입니다
```

하위 객체를 통해 메서드를 삭제하면 인스턴스 메서드 showInfo가 삭제된다. 인스턴스 메서드를 삭제한 상태에서 메서드를 다시 삭제해본다.

```
delete me.showInfo;

me.showInfo();// 23세 입니다
```

**하위 객체에서 프로토타입의 프로퍼티를 변경할 수 없다**

위 코드에서 알 수 있듯이 하위 객체를 통해 프로토타입의 프로퍼티를 변경 또는 삭제하는 것은 불가능하다. 다시 말해 하위 객체를 통해 프로토타입에 get 액세스는 허용되나 set액세스는 허용되지않는다.

**프로토타입 프로퍼티를 변경 / 삭제하는 방법**

프로토타입 프로퍼티를 변경 또는 삭제하려면 하위 객체를 통해 프로토타입 체인으로 접근하는 것이 아니라 프로토타입에 직접 접근해야 한다.

```
Student.prototype.showInfo = functioin() {
	console.log('안녕하세요 ' + this.age + '입니다');
};
me.showInfo(); // 안녕하세요 23세 입니다

delete Student.prototype.showInfo;
me.showInfo(); // TypeError: me.showInfo is not a function
```

## 9. 프로토타입의 교체

**프로토타입은 교체가능하다**

프로토타입은 임의의 다른 객체로 변경할 수 있다. 이것은 부모 객체인 프로토타입을 동적으로 변경할 수 있다는 것을 의미한다. 이러한 특징을 활용하여 객체 간의 상속 관계를 동적으로 변경할 수 있따. 프로토타입은 생성자 함수 또는 인스턴스에 의해 교체할 수 있다.

### 9.1 생성자 함수에 의한 프로토타입의 교체

**프로토타입을 직접 할당**

```
const Student = (function() {
	function Student(age) {
		this.age = age;
	}

	Student.prototype = {
		showInfo() {
			console.log(this.age + '세 입니다');
		}
	};

	return Student;
}());

const me = new Student(23);
```

Student.prototype에 객체리터럴을 할당했다. 이는 Student 생성자 함수가 생성할 객체의 프로톹아ㅣㅂ을 객체 리터럴로 교체한 것이다.

**프로토타입 교체 시 유의점**

프로토타입으로 교체한 객체 리터럴에는 constructor 프로퍼티가 없다. constructor 프로퍼티는 자바스크립트 엔진이 프로토타입을 생성할 때 암묵적으로 추가한 프로퍼티다. 따라서 me 객체의 생성자 함수를 검색하면 프로토타입 체인을 거슬러 올라가 Object.prototype의 constructor 프로퍼티를 검색하게 되어 Student가아닌 Object가 나온다.

```
console.log(me.constructor === Student); //false

console.log(me.constructor === Object); // true
```

- 프로토타입을 교체하면 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴된다.

  **constructor 프로퍼티와 생성자 함수간의 연결을 복구하는 법**

파괴된 constructor 프로퍼티와 생성자 함수 간의 연결을 되살리기 위해서는 다음 방법을 따른다.

- 프로토타입으로 교체한 객체 리터럴에 constructor 프로퍼티를 추가하여 프로토타입의 constructor 프로퍼티를 되살린다.

```
const Student = (function() {
	function Student(age) {
		this.age = age;
	}

	Student.prototype = {
		constructor: Student,
		showInfo() {
			console.log(this.age + '세 입니다');
		}
	};

	return Student;
}());

const me = new Student(23);
```

**결과**

```
console.log(me.prototype === Student); //true
console.log(me.prototype === Object); //false
```

### 9.2 인스턴스에 의한 프로토타입의 교체

**접근자 프로퍼티를 통한 프로토타입 교체**

프로토타입은 생성자 함수의 prototype 프로퍼티뿐만 아니라 인스턴스의 `__proto__` 접근자 프로퍼티나 빌트인 객체의 메서드를 통해 접근할 수 있다.

**프로퍼티에 직접 바인딩하는것과의 차이점**

생성자 함수의 prototype 프로퍼티에 다른 임의의 객체를 바인딩하는 것은 미래에 생성할 인스턴스의 프로토타입을 교체하는 것이다. `__proto__` 접근자 프로퍼티를 통해 프로토타입을 교체하는 것은 이미 생성된 객체의 프로토타입을 교체하는 것이다.

```
function Student(age) {
	this.age = age;
}

const me = new Student(23);

const parent = {
	showInfo() {
		console.log(`${this.age}세 입니다`);
	}
};

Object.setPrototypeOf(me, parent);

me.showInfo(); // 23세 입니다
```

```
// 프로토타입으로 교체한 객체에는 constructro 프로퍼티가 없다.
// constructor 프로퍼티와 생성자 함수간의 연결이 파괴된다.
// 프로토타입의 constructor 프로퍼티로 me 객체의 생성자 함수를 검색하면 Person 이 아닌 Object가 나온다

console.log(me.constructor === Student); // false
console.log(me.constructro === Object); //true
```

**차이점 정리**

- 생성자 함수에 의한 프로토타입 교체
  - Student 생성자 함수의 prototpype 프로퍼티가 교체된 프로토타입을 가리킨다.
- 인스턴스에 의한 프로토타입 교체
  - Student 생성자 함수의 prototype 프로퍼티가 교체된 프로토타입을 가리키지 않는다.

**인스턴스에 의한 프로토타입 교체 - 생성자 함수와의 연결 되살리기**

프로토타입으로 교체한 객체 리터럴에 constructor 프로퍼티를 추가하고 생성자 함수의 prototype 프로퍼티를 재설정하여 파괴된 생성자 함수와 프로토타입 간의 연결을 되살려 보자.

```
function Student(age) {
	this.age = age;
}

const me = new Student(23);

//constructor 프로퍼티 추가
const parent = {
	constructor: Student,
	showInfo() {
		console.log(`${this.age}세 입니다`);
	}
};

// prototype 연결
Student.prototype = parent;

Object.setPrototypeOf(me, parent);

me.showInfo(); // 23세 입니다

console.log(me.constructor === Student); // true
console.log(me.constructor === Object); //false

console.log(Student.prototype === Object.getPrototypeOf(me)); // true
```

**클래스의 도입**

프로토타입 교체를 통해 객체 간의 상속 관계를 동적으로 변경하는 것은 꽤나 번거롭다. 하지만 ES6에서 도입된 클래스를 사용하면 간편하고 직관적으로 상속 관계를 구현할 수 있다.

프로토타입 교체를 통해 객체 간의 상속 관계를 동적으로 변경하는 것은 번거롭다. 따라서 프로토타입은 직접 교체하지 않는 것이 좋다. 상속관계를 인위적으로 설정하려면 직접 상속이 더 편리하고 안전하다. 또는 ES6에서 도입된 클래스를 사용하면 간편하고 직관적으로 상속 관계를 구현할 수 있다.

## 10. instanceof 연산자

**instanceof 연산자란**

instanceof 연산자는 이항 연산자로서 좌변에 객체를 가리키는 식별자, 우변에 생성자 함수를 가리키는 식별자를 피연산자로 받는다. 만약 우변의 피연산자가 함수가 아닌 경우 TypeError가 발생한다

**instanceof 연산자 표현식의 평가값**

- Student.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true로 평가된다.
- Object.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true 로 평가된다.

```
function Student(age) {
	this.age = age;
}

const me = new Student(23);

console.log(me instanceof Student); // true

console.log(me instanceof Object); // true
```

**instanceof 연산자의 동작과정**

instanceof 연산자가 어떻게 상속 관계를 파악하는지, 인스턴스에 읳 프로토타입을 교체해보며 알아본다

```
function Student(age) {
	this.name = name;
}

const me = new Student(23);

const parent = {};

Object.setPrototypeOf(me, parent);

console.log(Student.prototype === parent);//false
console.log(parent.constructor === Student);//false

console.log(me instanceof Student); //false

console.log(me instanceof Object); //true


```

**프로토타입 교체시 생성자 함수와의 연결**

me 객체는 비록 프로토타입이 교체되어 프로토타입과 생성자 함수간의 연결이 Student 생성자 함수에 의해 생성된 인스턴스임에 틀림이 없다. 그러나 me instanceof Student 는 false 로 평가된다.

이는 Student.prototype이 me 객체의 프로토타입 체인상에 존재하지 않기 때문이다. 따라서 프로토타입으로 교체한 객체 parent 객체를 Student 생성자 함수의 prototype 프로퍼티에 바인딩하면 me instanceof Student는 true로 평가될 것이다.

**교체한 프로토타입과 생성자 함수와의 연결**

```
function Student(age) {
	this.age = age;
}

const me = new Student(23);

const parent = {};

Object.setPrototypeOf(me, parent);

console.log(Student.prototype === parent);//false
console.log(parent.constructor === Student);//false

Student.prototype = parent;

console.log(me instanceof Student); // true

console.log(me instanceof Object); //true
```

**instanceof 연산자의 원리**

이처럼 instanceof 연산자는 프로토타입의 constructor 프로퍼티가 가리키는 생성자 함수를 찾는 것이 아니라, 생성자 함수의 prototype 에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인한다.

instanceof 연산자는 좌변 피연산자의 프로토타입 체인 상에 우변의 피연산자, 즉 생성자 함수의 prototype 프로퍼티에 바인딩된 객체가 존재하는 지 검색한다.

me instanceof Student의 경우, me 객체의 프로토타입 체인 상에 Student.prototype에 바인딩된 객체가 존재하는지 확인한다.

me instnaceof Object 의 경우 me 객체의 프로토타입 체인 상에 Object.prototype에 바인딩된 객체가 존재하는지 확인한다. instanceof 연산자를 함수로 표현하면 다음과 같다.

```
function isInstanceof(instance, constructor) {
	const prototype = Object.getPrototypeOf(instance);

	if(prototype === null) return false;

	return prototype === constructor.prototype || isInstanceof(prototype, constructor);
 }

 console.log(isInstanceof(me, Student)) ; //true
 console.log(isInstanceof(me, Object)); true
 console.log(isInstanceof(me, Array)); // false
```

## 11. 직접 상속

### 11.1 Object.create에 의한 직접 상속

**Object.create 메서드의 동작**

Object.create 메서드는 명시적으로 프로토타입을 지정하여 새로운 객체를 생성한다. Object.create 메서드도 다른 객체 생성 방식과 마찬가지로 추상연산 OrdinaryObjectCreate를 호출한다.

Object.create 메서드의 첫 번째 매개변수에는 생성할 객체의 프로토타입으로 지정할 객체를 전달한다. 두 번째 매개변수에는 생성할 객체의 프로퍼티 키와 프로퍼티 디스크립터 객체로 이뤄진 객체를 전달한다. 이 객체의 형식은 Object.definePRoperties 메서드의 두 번째 인수와 동일하다. 두 번째 인수는 옵션이므로 생략가능하다.

```
Object.create(prototype, [propertiesObject])
```

**사용 예시**

```
let obj = Object.create(null);
console.log(Object.getPrototypeOf(obj) === null);

console.log(obj.toString()); // TypeError

obj = Object.create(Object.prototype);
console.log(Object.getPrototypeOf(obj) === Object.prototype); //true

obj = Object.create(Object.prototype,{
	x: { value: 1, writable: true, enumerable: true, configurable: true}
});

console.log(obj.x); //1
console.log(Object.getPrototypeOf(obj) === Object.prototype); //true

const myProto = { x: 10};

obj = Object.create(myProto);
console.log(obj.x);
console.log(Object.getPrototypeOf(obj) === myProto); //true

function Person(name) {
	this.name = name;
}

obj = Object.create(Person.prototype);
obj.name = 'Lee';
console.log(obj.name); //Lee
```

**Object.create 메서드의 장점**

Object.create 메서드는 첫 번째 매개변수에 전달한 객체의 프로토타입 체인에 속하는 객체를 생성한다. 즉, 객체를 생성하면서 직접적으로 상속을 구현하는 것이다. 이메서드의 장점은 다음과 같다.

- new 연산자가 없이도 객체를 생성할 수 있다.
- 프로토타입을 지정하면서 객체를 생성할 수 있다.
- 객체 리터럴에 의해 생성된 객체도 상속받을 수 있다.

**Object.prototype의 상속**

Object.prototype의 빌트인 메서드인 Object.prototype.hasOwnProperty, Object.prototype.isPrototypeOf, Object.prototype.propertyIsEnumerable 등은 모든 객체의 프로토타입 체인의 종점, 즉 Object.[rototype의 메서드이므로 모든객체가 상속받아 호출할 수 잇다.

```
const obj = {a: 1};

obj.hasOwnProperty('a'); // true

obj.propertyISEnumerable('a');// true
```

**주의점**

그런데 ESLint에서는 앞의 예제와 같이 Object.prototype의 빌트인 메서드를 객체가 직접 호출하는 것을 권장하지 않는다. 그 이유는 Object.create메서드를 통해 프로토타입 체인의 종점에 위치하는 객체를 생성할 수 있기 때문이다. 프로토타입 체인으ㅢ 종점에 위치하는 객체는 Object.prototype의 빌트인 메서드를 사용할 수 없다.

```
const obj = Object.create(null);
obj.a = 1;

console.log(Object.getPrototypeOf(obj)=== null) ; //true

console.log(obj.hasOwnProperty('a'));// TypeError: obj.hasOwnProperty is not a function

```

**Object.prototype 빌트인 메서드의 간접 호출**

따라서 이같은 에러를 발생시킬 위험을 없애기 위해 Object.prototype 의 빌트인 메서드는 다음과 같이 간접적으로 호출하는 것이 좋다.

```
const obj = Object.create(null);
obj.a = 1;

console.log(Object.prototype.hasOwnProperty.call(obj,'a')); //true
```

### 11.2 객체 리터럴 내부에서 `__proto__`에 의한 직접 상속

**Object.create의 단점**

Object.create 메서드에 의한 직접 상속은 앞에서 다룬 것과 같이 여러 장점이 있다. 하지만 두번째 인자로 프로퍼티를 정의하는 것은 번거롭다. 일단 객체를 생성한 이후 프로퍼티를 추가하는 방법도 있으나 깔끔하지는 않다.

**객체리터럴 내부에서의 직접상속 구현**

```
const myProto = { x: 10};

const obj = {
	y: 20,

	__proto__: myProto
};

console.log(obj.x, obj.y); // 10 20
console.log(Object.getPrototypeOf(obj) === myProto); //true
```

## 12. 정적 프로퍼티 / 메서드

**정적 프로퍼티 / 메서드란**

정적(static) 프로퍼티 / 메서드는 생성자 함수로 인스턴스를 생성하지 않아도 참조/호출할 수 있는 프로퍼티/메서드를 말한다.

```
function Student(age) {
	this.age = age;
}

//프로토타입 메서드
Student.prototype.showInfo = function () {
	console.log(this.age + '세 입니다');
};

//정적 프로퍼티
Student.staticProp = 'statick prop';

//정적 메서드
Student.staticMethod = function () {
	console.log('staticMethod');
};

const me = new Student(23);

Student.staticMethod();

me.staticMethod(); // TypeError
```

Student 생성자 함수는 객체이므로 자신의 프로퍼티/메서드를 소유할 수 있다. Student 생성자 함수 객체가 소유한 프로퍼티/메서드를 정적 프로퍼티/메서드라고 한다. 정적 프로퍼티/메서드는 생성자 함수가 생성한 인스턴스로 참조/호출할 수 없다.

**정적 프로퍼티/메서드의 접근가능성**

생성자 함수가 생성한 인스턴스는 자신의 프로토타입 체인에 속한 객체의 프로퍼티/메서드에 접근할 수 있따. 하지만 정적 프로퍼티/메서드는 인스턴스의 프로토타입 체인에 속한 프로퍼티/ 메서드가 아니므로 인스턴스로 접근할 수 없다.

**예시**

앞에서 살펴본 Object.create 메서드는 Object 생성자 함수의 정적 메서드고 Object.prototype.hasOwnProperty 메서드는 Object.prototype의 메서드다. 따라서 Object.create 메서드는 인스턴스, 즉 Object 생성자 함수가 생성한 객체로 호출할 수 없다.

하지만 Object.prototype.hasOwnProperty 메서드는 모든 객체의 프로토타입 체인의 종점, 즉 Object.prototype의 메서드이므로 모든 객체가 호출할 수 있다.

```
const obj = Object.create({ name: 'Lee'});

obj.hasOwnProperty('name');
```

**정적 메서드 사용이유**

인스턴스에서 메서드는 다른 데이터프로퍼티를 참조하거나 변경하는데 사용된다.

만약 인스턴스 / 프로토타입 메서드 내에서 this를 사용하지 않는다면 그 메서드는 정적 메서드로 변경할 수 있다. 인스턴스가 호출한 인스턴스/ 프로토타입 메서드내에서 this는 인스턴스를 가리킨다. 메서드 내에서 인스턴스를 참조할 필요가 없다면 정적 메서드로 변경해도 동작한다. 프로토타입 메서드를 호출하려면 인스턴스를 생성해야하지만 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있다.

```
function Foo() {}
Foo.prototype.x = function () {
	console.log('x');
};

const foo = new Foo();
//프로토타입 메서드를 호출하려면 인스턴스를 생성해야 한다.

foo.x(); //x

//정적 메서드
Foo.x = function() {
	console.log('x');
};

Foo.x();// x
//인스턴스를 생성하지 않아도 메서드를 호출할 수 있다.

```

## 13. 프로퍼티 존재 확인

### 13.1 in 연산자

**in 연산자의 기능**

in 연산자는 객체 내에 특정 프로퍼티가 존재하는 지 여부를 확인한다. in 연산자의 사용방법은 다음과 같다.

```
key in object
```

**사용 예시**

```
const person = {
	name: 'Lee',
	address: 'Seoul'
};

console.log('name' in person); // true
console.log('address' in person); //true
```

**주의점**

in 연산자는 확인 대상 객체의 프로퍼티뿐만 아니라확인 대상 객체가상속받은 모든 프로토타입의 프로퍼티를 확인하므로 주의가 필요하다. person 객체에는 toString이라는 프로퍼티가 없지만 다음 코드의 실행 결과는 true다.

```
console.log('toString' in person);
```

**이유**

이는 in 연산자가 person 객체에 속한 프로토타입 체인상에 존재하는 모든 프로토타입에서 toString 프로퍼티를 검색했기 때문이다. toString은 Object.prototype의 메서드다.

**Reflect.has 메서드**

in 연산자 대신 ES6에서 도임된 Reflect.has 메서드를 사용할 수도 있다. Reflect.has 메서드는 in 연산자와 동일하게 동작한다.

```
const person = { name: 'Lee'};

console.log(Reflect.has(person, 'name'));// true
```

### 13.2 Object.prototype.hasOwnProperty 메서드

Object.prototype.hasOwnProperty 메서드를 사용해도 객체에 특정프로퍼티가 존재하는지 확인할 수 있다.

```
console.log(person.hasOwnProperty('name')); //true
console.log(person.hasOwnProperty('age')); // false
```

**특징**

Object.hasOwnProperty 메서드는 이름에서 알 수 있듯이 인수로 전달받은 프로퍼티 키가 객체 고유의 프로퍼티 키인 경우에만 true를 반환하고 상속받은 프로토타입의 프로퍼티 키인 경우 false를 반환한다.

## 14. 프로퍼티 열거

### 14.1 for... in 문

**기능**

객체의 모든 프로퍼티를 순회하며 열거(enumeration)하려면 for...in 문을 사용한다.

```
for(변수선언문 in 객체) {...}
```

```
const person = {
	name: 'Lee',
	address: 'Seoul'
};

for ( const key in person) {
	console.log(key + ': ' + person[key]);
}
//name: Lee
//address: Seoul
```

**for ... in 문의 원리**

for ... in 문은 객체의 프로퍼티 개수만큼 순회하며 for... in 문의 변수 선언문에서 선언한 변수에 프로퍼티 키를 할당한다. 위 예제의 경우, person 객체에는 2개의 프로퍼티가 있으므로 객체를 2번 순회하면서 프로퍼티 키를 key 변수에 할당한 후 코드블록을 실행한다. 첫 번째 순회에서는 프로퍼티 키 'name'을 key 변수에 할당한 후 코드블록을 실행하고 두 번째 순회에서는 프로퍼티 키 'address'를 key 변수에 할당한 후 코드 블록을 실행한다.

**Object.prototype의 프로퍼티가 열거되지 않는이유**

for ... in 문은 in 연산자 처럼 순회 대상 객체의 프로퍼티 뿐만 아니라 상속받은 프로토타입의 프로퍼티까지 열거한다. 하지만 toString 같은 Object.prototype의 프로퍼티가 열거되지 않는다.

```
const person = {
	name: 'Lee',
	address: 'Seoul'
};

console.log('toString' in person); //true

for (const key in person) {
	console.log(key + ': ' + person[key]);
}
//name: Lee
//address: Seoul
```

이는 toString 메서드가 열거할 수 없도록 정의되어 있는 프로퍼티이기 때문이다. 다시말해, Object.prototype.string 프로퍼티의 프로퍼티 어트리뷰트 [[Enumerable]] 의 값이 false이기 때문이다. 프로퍼티 어트리뷰트 [[Enumerable]] 은 프로퍼티의 열거 가능 여부를 나타내며 불리언 값을 갖는다

**for ... in 문의 기능에대한 정확한 표현**

for ... in 문은 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로퍼티 중에서 프로퍼티 어트리뷰트 [[Enumerabl]]의 값이 true인 프로퍼티를 순회하며 열거(enumeration) 한다.

```
const person = {
	name: 'Lee',
	address: 'Seoul',
	__proto__: { age: 20}
};

for (const key in person) {
	console.log(key + ': ' + person[key]);
}
//name: Lee
//address: Seoul
//age: 20
```

**예외**

for ... in 문은 프로퍼티 키가 심벌인 프로퍼티는 열거하지 않는다.

```
const sym = Symbol();
const obj = {
	a: 1,
	[sym]: 10
};

for (const key in obj) {
	console.log(key + ': ' + obj[key]);
}
//a: 1
```

**객체 자신의 프로퍼티만을 열거하는 방법**

상속받은 프로퍼티는 제외하고 객체 자신의 프로퍼티 만을 열거하려면 Object.prototype.hasOwnProperty 메서드를 사용하여 객체 자신의 프로퍼티인지 확인해야한다.

```
const person = {
	name: 'Lee',
	address: 'Seoul',
	__proto__: {age: 23}
};

for(const key in person) {
	if(!person.hasOwnProperty(key)) continue;
	console.log( key + ': ' + person[key]);
}
```

**for ... in 문의 순서**

위 예제의 결과는 person 객체의 프로퍼티가 정의된 순서대로 열거되었다. 하지만 for...in 문은 프로퍼티를 열거할 때 순서를 보장하지 않으므로 주의해야한다. 하지만 대부분의 모던 브라우저는 순서를 보장하고 숫자(사실은 문자열) 인 프로퍼티 키에 대해서는 정렬을 실시한다.

```
const obj = {
	2: 2,
	3: 3,
	1: 1,
	b: 'b',
	a: 'a'
};

for(const key in obj) {
	if(!person.hasOwnProperty(key)) continue;
	console.log( key + ': ' + obj[key]);
}
/*
1: 1
2: 2
3: 3
b: b
a: a
*/
```

**배열의 요소열거**

배열에는 for in 문을 사용하지말고 일반적인 for 문이나 for of 문 또는 Array.prototype.forEach 메서드를 사용하는것이좋다. 사실 배열도 객체이므로 프로퍼티와 상속받은 프로퍼티가 포함될 수 있다.

```
const arr = [1, 2, 3];
arr.x = 10;

for (const i in arr) {
	console.log(arr[i]); // 1 2 3 10
}

for (let i = 0; i < arr.length; i++) {
	console.log(arr[i]);
}

arr.forEach(v => console.log(v));

for (const value of arr) {
	console.log(value);
}
```

### 14.2 Object.keys/value/entries 메서드

**객체 자신의 고유프로퍼티만을 열거**

for in 문은 객체 자신의 고유 프로퍼티 뿐만 아니라 상속받은 프로퍼티도 열거한다. 따라서 Object.prototype.hasOwnProperty 메서드를 사용하여 객체 자신의 프로퍼티인지 확인하는 추가 처리가 필요하다.

객체 자신의 고유 프로퍼티만을 열거하기위해서는 for in 문을 사용하는 것보다 Object.keys/value/entries 메서드를 사용하는것이 좋다.

**Object.keys 메서드**

Object.keys 메서드는 객체 자신의 열거 가능한(enumerable) 프로퍼티 키를 배열로 반환한다.

```
const person = {
	name: 'Lee',
	address: 'Seoul',
	__proto__: { age: 20}
};

console.log(Object.keys(person)); ['name', 'address']
```

**Object.values 메서드**

ES8에서 도입된 Object.values 메서드는 객체 자신의 열거 가능한 프로퍼티 값을 배열로 반환한다.

```
console.log(Object.values(person)); // ['Lee', 'Seoul']
```

**Object.entries 메서드**

Object.entries 메서드는 객체 자신의 열거 가능한 프로퍼티 키와 값의 쌍의 배열을 배열에 담아 반환한다

```
console.log(Object.entries(person));
```
