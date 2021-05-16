---
title: javascript 17Constructor
date: 2020-09-24 21:26:53
category: "javascript"
draft: false
---

# 생성자 함수에 의한 객체 생성

## 1. Object 생성자 함수

**생성자 함수란**

생성자 함수(constructor)란 new 연산자와 함께 호출하여 객체(instance)를 생성하는 함수를 말한다. 생성자 함수에 의해 생성된 객체를 인스턴스(instance)라고 한다.

**Object 생성자 함수에 의한 객체 생성**

```
const person = new Object();

person.name = 'Jeong';
person.sayHello = function () {
	console.log(`My name is ${this.name}`);
};

console.log(person); //{name: 'Jeong', sayHello: f}
```

**자바스크립트의 빌트인(built in, 내장) 생성자 함수**

자바스크립트는 Object 생성자 함수 이외에도 String, Number, Boolean, Function, Array, Date, RegExp, Promise 등의 빌트인 생성자 함수를 제공한다.

```
// String 생성자 함수
const strObj = new String('Jeong');
console.log(strObj); //[String: 'Jeong']

//Number 생성자 함수
const numObj = new Number(111);
console.log(numObj); // [Number: 111]

//Boolean 생성자 함수
const boolObj = new Boolean(true); // [Boolean: true]

//Function 생성자 함수
const func = new Function('x', 'return x * x');

//Array 생성자 함수
const arr = new Array(1,3,5);

//RegExp 생성자 함수
const regExp = new RegExp(/ab+c/i);

//Date 생성자 함수
const date = new Date();
```

## 2. 생성자 함수

### 2.1 객체 리터럴에 의한 객체 생성 방식의 문제점

**객체를 여러개 생성하기 번거롭다**

객체 리터럴에 의한 객체 생성 방식은 직관적이고 간편하다. 하지만객체 리터럴에 의한 객체 생성 방식은 단 하나의 객체만 생성한다.

동일한 프로퍼티를 갖는 객체를 여러개 생성해야 하는 경우 매번 같은프로퍼티를 기술해야 하기 때문에 비효율적이다.

```
const circle1 = {
	radius: 5,
	getDiameter() {
		return 2 * this.radius;
	}
};

console.log(circle1.getDiameter()); //10

const circle2 = {
	radius: 10,
	getDiamter() {
		return 2 * this.radius;
	}
};

console.log(circle2.getDiameter()); // 20
```

동일한 객체를 여러개 생성한다면, 같은 내용의 메서드를 여러번 기술해야되는 번거로움이 있다.

**메서드는 동일한 경우가 많다**

객체는 프로퍼티를 통해 객체 고유의 상태(state)를 표현한다. 그리고 메서드를 통해 상태 데이터인 프로퍼티를 참조하고 조작하는 동작(behavior)을 표현한다. 객체마다 프로퍼티 값이 다를 수 있찌만 메서드는 내용이 동일한 경우가 일반적이다.

### 2.2 생성자 함수에 의한 객체 생성 방식의 장점

**간편하게 동일한 구조의 객체를 여러개 생성 가능하다.**

생성자 함수에 의한 객체 생성 방식은 마치 객체(instance)를 생성하기 위한 템플릿 (클래스)처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.

```
function Circle(radius) {
	this.radius = radius;
	this.getDiameter = function () {
		return 2 * this.radius;
	};
}

const circle1 = new Circle(5);
console.log(circle1.getDiameter());// 10

const circle2 = new Circle(10);
console.log(circle2.getDiameter()); // 20
```

**this 바인딩은 함수 호출 방식에 따라 결정된다.**

- 일반 함수로 호출
  - 전역객체에 바인딩
- 메서드로 호출
  - 메서드를 호출한 객체
- 생성자 함수로 호출
  - 생성자 함수가 생성할 인스턴스

**생성자 함수는 일반함수와 호출 방식에 차이가 있다**

생성자 함수는 이름 그대로 객체(인스턴스)를 생성하는 함수다. 하지만 자바와 같은 클래스 기반 객체지향 언어의 생성자(constructor)와는 다르게 그 형식이 정해져 있는 것이 아니라 일반 함수와 동일한 방법으로 생성자 함수를 정의한다.

일반함수와는 호출방식에서 차이가 있다.

- new 연산자와 함께 호출
  - 생성자 함수로 동작
- new 연산자 없이 호출
  - 일반 함수로 동작

```
function Rectangle(width = 1, height = 1) {
	this.width = width;
	this.height = height;

	this.getArea(){
		return this.width * this.height;
	};
}
//일반함수로 호출 시 this는 전역 객체를 가리킨다.
const rect1 = Rectangle(2, 3);
console.log(width); // 2
console.log(heigth); // 3
getArea();// 6

```

### 2.3 생성자 함수의 인스턴스 생성 과정

**인스턴스 생성과 초기화**

생성자 함수의 함수 몸체에서 수행해야 하는 것이 무엇인지 생각해보자. 생성자 함수의 역할은 프로퍼티 구조가 동일한 인스턴스를 생성하기 위한 템플릿(클래스)으로서 동작하여 인스턴스를 생성하는 것과 생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기값 할당)하는 것이다.

생성자 함수가 인스턴스를 생성하는 것은 필수이고, 생성된 인스턴스를 초기화하는 것은 옵션이다.

```
function Rectangle(width = 1, height = 1) {
	//인스턴스 초기화
	this.width = width;
	this.height = height;

	this.getArea(){
		return this.width * this.height;
	};
}

//인스턴스 생성
const rect1 = new Rectangle( 3, 4); 가로3 세로4인 객체 생성
```

**인스턴스는 암묵적으로 생성되고 반환된다.**

생성자 함수의 내부 코드를 보면 this에 프로퍼티를 추가해서 초기화하는 것을 알 수 있다. 하지만 인스턴스를 생성하는 코드는 보이지 않는다.

자바스크립트 엔진은 암묵적인 처리를 통해 인스턴스를 생성하고 반환한다.

new 연산자와 함께 생성자 함수를 호출하면 자바스크립트 엔진은 다음과 같은 과정을 거쳐 암묵적으로 인스턴스를 생성하고 인스턴스를 초기화한 후 암묵적으로 인스턴스를 반환한다.

**1. 인스턴스 생성과 this 바인딩**

new 연산자와 함깨 생성자 함수가 호출 되면 암묵적으로 빈 객체가 생성된다. 이 빈 객체가 생성자 함수가 생성한 인스턴스이며, 이 빈 객체는 this에 바인딩된다.

즉 생성자 함수의 내부의 this는 생성할 인스턴스를 가리킨다.

이 처리는 런타임 이전에 실행된다.

**바인딩(binding)이란**

바인딩(name binding)이란 식별자와 값을 연결하는 과정을 의미한다.

변수 선언의 경우 변수이름과 확보된 메모리공간을 바인딩하는 것이다. this는 키워드이지만 식별자 역할을 한다. this 바인딩은 this와 this가 가리킬 객체를 바인딩하는 것이다.

```
function Rectangle(width = 1, height = 1) {
	// 1. 런타임 이전에 암묵적으로 빈 객체가 생성되고 this에 바인딩된다.
	this.width = width;
	this.height = height;

	this.getArea(){
		return this.width * this.height;
	};
}
new Rectangle(2,3);
```

**2. 인스턴스 초기화**

생성자 함수에 기술되어 있는 코드가 한 줄씩 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다.

this에 바인딩되어 있는 객체에 프로퍼티와 메서드를 추가하고 인수로 전달받은 초기값을 바인딩된 인스턴스의 프로퍼티에 할당한다.

```
function Rectangle(width = 1, height = 1) {
	// 1. 런타임 이전에 암묵적으로 빈 객체가 생성되고 this에 바인딩된다.

	// 2. this에 바인딩된 인스턴스를 초기화한다.
	this.width = width;
	this.height = height;

	this.getArea(){
		return this.width * this.height;
	};
}
new Rectangle(2,3);
```

**3. 인스턴스 반환**

생성자 함수의 모든 문이실행되고 인스턴스의 생성, 초기화가 끝나면 자바스크립트 엔진은 암묵적으로 해당 인스턴스를 반환한다.

```
function Rectangle(width = 1, height = 1) {
	// 1. 런타임 이전에 암묵적으로 빈 객체가 생성되고 this에 바인딩된다.

	// 2. this에 바인딩된 인스턴스를 초기화한다.
	this.width = width;
	this.height = height;

	this.getArea(){
		return this.width * this.height;
	};
	//3. this에 바인딩된 인스턴스 암묵적 반환
}
new Rectangle(2,3);
```

**return 값을 명시한다면?**

만약 this가 아닌 다른 객체를 명시적으로 반환하면 this에 바인딩된 인스턴스가 반환되는 것이 아니라, 명시적으로 기술한 객체가 반환된다.

```
function Rectangle(width = 1, height = 1) {
	// 1. 런타임 이전에 암묵적으로 빈 객체가 생성되고 this에 바인딩된다.

	// 2. this에 바인딩된 인스턴스를 초기화한다.
	this.width = width;
	this.height = height;

	this.getArea(){
		return this.width * this.height;
	};
	//3.this에 바인딩된 인스턴스 암묵적 반환

	//객체를 명시적으로 반환시 this반환이 무시된다.
	return {};
}
const rect1 = new Rectangle(2,3);

console.log(rect1);//{}
```

**원시값을 반환한다면** 원시값반환이 무시되고 암묵적으로 this가 반환된다.

결론적으로 생성자 함수를 만들 때 return 문을 사용하면 안된다. 생성자 함수의 기본 동작을 훼손하기 때문이다.

### 2.4 내부 메서드 [[Call]]과 [[Construct]]

**함수는 일반 객체와 동일하게 동작할 수 있다.**

함수 선언문 또는 함수 표현식으로 정의한 함수는 일반 함수로 호출할 수 있으며, 생성자 함수로서 호출할 수도 있다.

생성자 함수로 호출하는 것은 new 연산자와 함께 함수를 호출하여 객체를 생성하는 것이다.

함수는 객체이므로 일반 객체(ordinary object)와 동일하게 동작할 수 있다. 함수 객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드를 모두 가지고 있기 때문이다.

```
function foo() {}
//함수는 객체이므로 프로퍼티를 소유할 수 있다
foo.name = 'Jiman';
//메서드도 소유할 수 있다.
foo.getName = function() {return this.name};

console.log(foo.getName()); //Jiman
```

**함수와 일반 객체의 차이점**

함수는 객체이지만 일반 객체와는 다르다. 일반객체는 호출할 수 없지만 함수는 호출할 수 있다.

함수는 일반 객체가 가진 내부 슬롯과 내부메서드를 가지고 있고, 추가로 함수로 동작하기 위한 내부 슬롯과 내부메서드를 가지고 있다.

함수 객체만을 위한 내부 슬롯,메서드 예시

- 내부슬롯
  - [[Environment]], [[FormalParameters]] 등
- 내부 메서드
  - [[Call]], [[Construct]] 등

```
function foo() {}

foo(); // 내부 메서드 [[Call]] 호출

new foo(); // 내부메서드 [[Construct]] 호출
```

**함수객체의 내부 메서드**

내부 메서드 [[Call]] 을 갖는 함수 객체를 callable이라 하며, 내부 메서드 [[Construct]]를 갖는 함수 객체를 constructor, [[Construct]]를 갖지 않는 객체를 non-constructor 이라고 부른다.

callable은 호출할 수 있는 객체, 즉 함수를 말한다.

constructor는 생성자 함수로서 호출할 수 있는 함수, non-constructor는 객체를 생성자 함수로서 호출할 수 없는 함수를 의미한다.

호출이 가능한 것은 함수 객체가 되기위한 필요조건이다. 즉 모든 함수 객체는 내부메서드 [[Call]] 을 가져서 callable 이어야한다.

단, 모든 함수 객체가 [[Construct]]를 갖는 것은 아니다. 모든 함수는 호출 가능하지만, 모든 함수가 생성자 함수로서 호출가능하진 않다.

- 모든 함수는 callable이다.
- constructor인 함수도 있고 non-constructor인 함수도 있다

### 2.5 constructor와 non-constructor의 구분

**함수 정의 방식에 따른 constructor 구분**

자바스크립트 엔진이 어떻게 constructor와 non-constructor를 구분하는지 살펴보자. 자바스크립트 엔진은 함수 정의를 평가하여 함수객체를 생성할 때, 함수 정의 방식에 따라 함수를 constructor과 non-constructor로 구분한다.

- constructor : 함수 선언문, 함수 표현식, 클래스
- non-constructor : 메서드(ES6메서드 축약 표현), 화살표 함수
  - 메서드는 메서드 축약표현만을 인정한다.

```
//constructor
//일반 함수 정의: 함수 선언문, 함수 표현식

function foo() {}
const bar = function () {};
const baz = {
	f: function(){}
};
//baz의 프로퍼티 f에 할당된 함수는 일반적인 의미로는 메서드이지만 ES6에서는 메서드로 인정하지 않는 일반함수이다.

//일반 함수로 정의된 함수는 constructor
new foo();
new bar();
new baz.f();

//non-constructor
//화살표 함수, 메서드

const arrow = () => {};
const obj = {
	f(){} //축약표현만이 메서드로 인정
};

//constructor 가 아니다, 에러 발생
new arrow();
new obj.f();
//TypeError: arrow(obj.f) is not a constructor
```

**ECMAScript 사양에서의 메서드**

일반적으로 함수를 프로퍼티 값으로 사용하면 메서드로 통칭한다. 그러나 ECMAScript 사양에서는 메서드란 ES6의 메서드 축약표현을 의미한다. 즉 메서드는 다음 조건을 만족해야한다.

- 함수를 프로퍼티 값으로 사용
- 메서드 축약표현으로 기술

**함수의 호출방식에 따른 내부 메서드 동작**

함수를 일반 함수로 호출했을때와 new 연산자와 함께 생성자 함수로 호출했을 때 호출되는 내부메서드가 다르다

- 일반 함수로서 호출
  - [[Call]] 호출
- 생성자 함수로서 호출
  - [[Constructor]] 호출
  - non-constructor 호출 시 에러

**주의점**

일반함수로 사용할 것을 목적으로 정의한 일반함수를 new 연산자와 호출하면 목적과는 달리 생성자 함수로 동작할 수 있다.

### 2.6 new 연산자

**new 연산자를 통한 호출방식 구분**

일반 함수와 생성자 함수에 특별한 형식적 차이는 없다. new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다. 다시 말해, 함수 객체의 내부 메서드 [[Call]] 이 호출되는 것이 아니라 [[Construct]]가 호출된다.

new 연산자와 함께 호출하는 함수는 constructor 이어야 한다.

```
//생성자 함수로서 정의하지 않은 일반 함수
function foo(){return 100;}
const obj1 = new foo();

console.log(obj1);//{} 원시값을 반환하는 return 문이 무시되고 빈 객체가 할당

function bar() { return [1, 2]}
const obj2 = new bar();

console.log(obj2);// [1, 2] return 문이 객체를 반환하므로 해당 객체를 반환
```

**생성자 함수를 new 연산자 없이 호출한다면**

new 연산자 없이 생성자 함수를 호출하면 일반함수로 호출된다. 즉, 내부 메서드 [[Construct]]가 아닌 [[Call]]이 호출된다.

```
//생성자 함수
function Rectangle(width, height) {
	this.width = width,
	this.height = height,
	this.getArea = function () {
		return width * height;
	}
}

const rect1 = Rectangle(5,5);

console.log(rect1); //undefined
// 반환문이 없는 일반함수는 undefined를 반환한다.

//일반함수 내부의 this는 전역객체가 된다.
console.log(width); 5
console.log(getArea()) ; //25

console.log(rect1.getArea()); //TypeError
```

**생성자 함수의 표기**

일반함수와 생성자함수에 특별한 형식적 차이는 없다. 그렇기 때문에 의도적으로 생성자 함수를 기술할 때 파스칼케이스로 명명하여 차이를 두도록 하자

### 2.7 new.target

**생성자 함수의 일반함수 호출 방지**

생성자 함수가 new 연산자 없이 호출되는 것을 방지하기 위해 파스칼 케이스 컨벤션을 사용하다 하더라도 실수는 언제나 발생할 수 있다.

이러한 위험성을 피하기 위해 ES6 에서는 new.target을 지원한다.

new.target은 this와 유사하게 constructor인 모든 함수 내부에서 암묵적인 지역 변수와 같이 사용되며 메타 프로퍼티라고 부른다. IE는 new.target 을 지원하지 않는다

new.target을 함수 내부에서 사용하면 해당 함수가 new 연산자와 함께 호출되었는지 확인가능하다.

- new 연산자와 함께 생성자 함수로서 호출된경우
  - new.target은 함수 자신을 가리킨다
- new 연산자 없이 일반 함수로서 호출된 경우
  - new.target 은 undefined 이다
  - 일반함수로 호출한 경우 재귀호출로 new와 함께 호출한다.

```
//생성자 함수

function Book(title,author){
	if(!new.target){
		return new Book(title, author);
	}
	this.title = title;
	this.author = author;

	this.getInfo = function(){
		return this.title + ', '+this.author;
	};
}

const book1 = Book('어린왕자', '생택쥐베리');

console.log(book1); // {title: ....}
```

**스코프 세이프 생성자 패턴(scope-safe constructor**

ES6의 문법인 new.target을 사용할 수 없을때 사용한다.

```
function Book(title,author){
	if(!this instanceof Book){
		return new Book(title, author);
	}
	this.title = title;
	this.author = author;

	this.getInfo = function(){
		return this.title + ', '+this.author;
	};
}
```

**빌트인 생성자 함수와 new**

- Object, Function
  - new 없이 호출하여도 new와 함께 호출한 것처럼 동작
- String, Number, Boolean
  - new 없이 호출하면 문자열, 숫자, 불리언 값을 반환
