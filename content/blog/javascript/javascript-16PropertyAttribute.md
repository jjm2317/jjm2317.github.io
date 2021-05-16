---
title: javascript 16PropertyAttribute
date: 2020-09-23 22:53:27
category: "javascript"
draft: false
---

# 프로퍼티 어트리뷰트

## 1. 내부 슬롯과 내부 메서드

**자바스크립트 엔진 내부는?**

자바스크립트로 작성한 코드는 자바스크립트 엔진에 의해 해석되고 실행된다. 자바스크립트 엔진도 코드를 실행하기 위해 코딩된 하나의 프로그램이라고 할 수 있다. 자바 스크립트 엔진은 객체지향 언어 C++ 로 코딩되어 있다. 즉 엔진 내부에도 프로그램 구현을 위한 알고리즘이 있다는 이야기이다 .

**내부 슬롯, 내부 메서드란**

내부 슬롯(internal slot) 과 내부 메서드 (internal method)는 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티(pseudo property) 와 의사 메서드(pseudo method) 이다. ECMAScript 사양 에서는 내부슬롯과 내부 메서드를 이중 대괄호( [[]] )로 해당 이름을 감싸서 표현하고 있다.

**내부 슬롯, 내부 메서드의 특징**

내부 슬롯과 내부 메서드는 ECMAScript 사양에 정의된 대로 구현되어 자바스크립트 엔진에서 실제로 동작한다. 하지만 개발자가 직접 접근할 수 있도록 외부로 공개된 객체의 프로퍼티는 아니다.

내부슬롯과 내부메서드는 자바스크립트 엔진의 내부 로직이므로 원칙적으로 자바스크립트는 내부슬롯과 내부메서드에 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않는다. 괜한 문제나 어려움을 유발하지 않기 위해서이다.

단, 일부 내부 슬롯과 내부 메서드에 한하여 **간접적으로** 접근할 수 있는 수단을 제공한다.

```
// 모든 객체는 [[Prototype]] 이라는 내부슬롯을 갖는다
// 직접 접근은 불가하며 접근자 프로퍼티로 간접 접근은 가능하다.

const obj = {};

o.[[Prototype]]; // Uncaught SyntaxError

o.__proto__ // Object.prototype
```

## 2. 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

**프로퍼티 어트리뷰트란**

자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.

프로퍼티의 상태란 다음과 같다.

- 값(value)
- 값의 갱신 가능 여부(writable)
- 열거 가능 여부(enumerable)
- 재정의 가능 여부(configurable)

프로퍼티 어트리뷰트는 자바스크립트 엔진이 관리하는 내부 상태 값(meta-property)인 내부 슬롯 [[Value]], [[Writable]], [[Enumerable]], [[Configurable]]를 말한다.

**프로퍼티의 어트리뷰트에 접근하는 법**

프로퍼티 어트리뷰트 역시 직접접근은 불가하다.

간접적으로 접근하기 위해 Object.getOwnPropertyDiscriptor 메서드를 사용한다.

```
const car = {
	price: 5000
};

Object.getOwnPropertyDiscriptor(car, 'price');
//{value: 5000, writable: true, enumerable: true, configurable: true}
```

메서드를 호출할 때 첫 번째 매개변수에는 객체의 식별자, 두번째는 프로퍼티 키를 문자열로 전달한다.

**주의할 점**

- 프로퍼티 키는 식별자가 아닌 문자열이다. 인수 전달에 주의해야한다.

**반환 값**

Object.getOwnPropertyDiscriptor 메서드는 프로퍼티 어트리뷰트 정보를 프로퍼티로서 가지는 **프로퍼티 디스크립터(PropertyDescriptor)객체**를 반환한다.

- 존재하지 않는 프로퍼티를 인수로 전달할 경우
  - undefined를 반환
- 상속받은 프로퍼티를 인수로 전달할 경우
  - undefined 반환

**모든 프로퍼티의 내부 상태를 알고 싶다면**

Object.getOwnPropertyDiscriptor 메서드의 경우 하나의 프로퍼티의 디스크립터 객체를 반환한다.

ES8에서 도입된 Object.getOwnPRopertyDescriptors 메서드는 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공한다.

```
const car = {
	price: 5000,
	brand: 'Hyundai'
};

Object.getOwnPropertyDiscriptors(car);
//{
	price: {value: 5000, writable: true, enumerable: true, 	configurable: true},
	brand: {value: 'Hyundai', writable: true, enumerable: true, configurable: true}
}
```

## 3. 데이터 프로퍼티와 접근자 프로퍼티

**프로퍼티의 구분**

프로퍼티는 데이터 프로퍼티와 접근자 프로퍼티로 구분할 수 있다.

- 데이터 프로퍼티(data property)
  - 키와 값으로 구성된 일반적인 프로퍼티다.
  - 지금까지 살펴본 모든 프로퍼티는 데이터 프로퍼티다.
- 접근자 프로퍼티(accessor property)
  - 자체적으로 값을 갖지 않는다
  - 다른 데이터 프로퍼티의 값을 **읽거나 저장**할 때 호출되는 접근자 함수(accessor function) 로 구성된 프로퍼티다.

### 3.1 데이터 프로퍼티

**데이터 프로퍼티의 프로퍼티 어트리뷰트**

데이터 프로퍼티(data property)는 다음과 같은 프로퍼티 어트리뷰트를 갖는다. 이 프로퍼티 어트리뷰트는 자바스크립트 엔진이 프로퍼티를 생성할 때 기본값으로 자동 정의된다.

| 프로퍼티 어트리뷰트 | 프로퍼티 디스크립터 객체의 프로퍼티 | 설명                                                                                                                                                                                                                                                                             |
| ------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [[Value]]           | value                               | - 프로퍼티 키를 통해 프로퍼티 값에 접근하면 반환되는 값이다. <br />- 프로퍼티 키를 통해 프로퍼티 값을 변경하면 [[Value]]에 값을 재할당<br />- 이때 프로퍼티가 없으면 프로퍼티를 동적 생성 후 생성된 프로퍼티의 [[Value]]에 값을 저장                                             |
| [[Writable]]        | writable                            | - 프로퍼티 값의 변경 가능 여부를 나타내며 불리언 값을 갖는다<br />- [[Writable]] 의 값이 false인 경우 해당 프로퍼티의 [[Value]]의 값을 변경할 수 없는 읽기 전용 프로퍼티가 된다.                                                                                                 |
| [[Enumerable]]      | enumerable                          | - 프로퍼티의 열거 가능여부를 나타내며 불리언 값을 갖는다<br />- [[Enumerable]]의 값이 false인 경우 해당 프로퍼티는 for...in 문이나 Object.keys 메서드 등으로 열거할 수 있다                                                                                                      |
| [[Configurable]]    | configurable                        | - 프로퍼티의 재정의 가능 여부를 나타내며 불리언 값을 갖는다<br />- [[Configurable]]의 값이 false인 경우 해당 프로퍼티의 삭제, 프로퍼티 어트리뷰트 값의 변경이 금지된다. <br />- 단 [[Writable]]의 true 인경우 [[Value]] 의 변경과 [[Writable]]을 false로 변경하는 것은 허용된다. |

```
const car = {
	price: 1000
};
//데이터프로퍼티의 디스크립터 객체 반환
console.log(Object.getOwnPropertyDiscriptor(car, 'price'));
//{value: 1000, writable: true, enumerable: true, configurable: true}

//프로퍼티 동적추가
car.brand = 'Hyundai';

console.log(Object.getOwnPropertyDescriptors(car));
//{
  price: { value: 1000, writable: true, enumerable: true, configurable: true },
  brand: {
    value: 'Hyundai',
    writable: true,
    enumerable: true,
    configurable: true
  }
}
```

리터럴로 객체를 생성하는 경우,

프로퍼티가 생성될 때 [[Value]] 는 프로퍼티 값으로, 나머지는 true로 초기화된다.

프로퍼티를 동적 추가해도 마찬가지이다.

### 3.2 접근자 프로퍼티

**접근자 프로퍼티란**

접근자 프로퍼티(accessor property)는 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용되는 접근자 함수(accessor function) 으로 구성된 프로퍼티이다.

**접근자 프로퍼티의 프로퍼티 어트리뷰트**

| 프로퍼티 어트리뷰트 | 프로퍼티 디스크립터 객체의 프로퍼티 | 설명                                                                                                                                                                                                                                     |
| ------------------- | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [[Get]]             | get                                 | - 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 **읽을 때** 호출되는 접근자 함수이다.<br />- 접근자 프로퍼티 키로 프로퍼티 값에 접근하면 프로퍼티 어트립뷰트 [[Get]]의 값, 즉 getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환된다. |
| [[Set]]             | set                                 | - 접근자 프로퍼티를 통해 데이터프로퍼티의 값을 저장할 때 호출되는 접근자 함수이다.<br />- 즉, 접근자 프로퍼티 키로 프로퍼티 값을 저장하면 프로퍼티 어트리뷰트 [[Set]]의 값, setter 함수가 호출되고 그 결과가 프로퍼티 값으로 저장된다.   |
| [[Enumerable]]      | enumerable                          | 데이터 프로퍼티와 동일                                                                                                                                                                                                                   |
| [[Configurable]]    | configurable                        | 데이터 프로퍼티와 동일                                                                                                                                                                                                                   |

**접근자 함수의 정의**

접근자 함수는 getter / setter 함수라고도 부른다. 접근자 프로퍼티는 getter와 setter 함수를 모두 정의할 수도 있고 하나만 정의할 수도 있다.

```
const person = {
	//데이터 프로퍼티
	firstName: 'Jiman',
	lastName: 'Jeong',

	//접근자 프로퍼티

	get fullName() {
		return `${this.firstName} ${this.lastName}`;
	},

	set fullName(name){
		[this.firstName, this.lastName] = name.split(' ');
	}
};

// setter 함수의 사용
person.fullName = 'Chansung Jeong';

console.log(person.firstName, person.lastName);
//Chansung Jeong

//getter 함수 사용
console.log(person.fullName)
Chansung Jeong
```

**접근자 프로퍼티의 동작 원리**

내부슬롯, 메서드 관점에서, 접근자 프로퍼티 fullName으로 프로퍼티 값에 **접근**하면 내부적으로 [[Get]] 내부 메서드가 호출된다.

[[Get]] 내부 메서드의 동작

1. 프로퍼티 키가 유효한지 확인한다. 프로퍼티 키는 문자열 또는 심벌이어야 한다
2. 프로토 타입 체인에서 프로퍼티를 검색한다.
3. 검색된 프로퍼티가 데이터 프로퍼티인지, 접근자 프로퍼티인지 확인한다.
4. 접근자 프로퍼티의 프로퍼티 어트리뷰트 [[Get]]의 값인 getter 함수를 호출하여 결과를 반환한다. [[Get]]의 값은 해당 프로퍼티의 디스크립터 객체의 get 프로퍼티 값과 같다

**데이터 프로퍼티와 접근자 프로퍼티를 구별하는 법**

- Object.getOwnPropertyDiscriptor 메서드가 반환한 프로퍼티 어트리뷰트 정보를 확인한다.

## 4. 프로퍼티 정의

**프로퍼티 정의란**

프로퍼티 정의란 프로퍼티 어트리뷰트를 정의하는 것이다.

- 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의
- 기존 프로퍼티의 프로퍼티 어트리뷰트 재정의

프로퍼티를 정의함으로서 객체의 프로퍼티가 어떻게 동작해야 하는 지 명확히 정의할 수 있다.

**프로퍼티 어트리뷰트를 정의하는 법**

Object.defineProperty 메서드를 사용하면 프로퍼티의 어트리뷰트를 정의할 수 있다. 인수로는 객체의 참조와 데이터 프로퍼티의 키인 문자열, 프로퍼티 디스크립터 객체를 전달한다.

```
const person = {};

//데이터 프로퍼티 정의
Object.defineProperty(person, 'firstName', {
	value: 'Jiman',
	writable: true,
	enumerable: true,
	configurable: true
} );
Object.defineProperty(person, 'lastName', {
	value: 'Jeong',
});

console.log(Object.getOwnPropertyDescriptors(person));
//{
  firstName: {
    value: 'Jiman',
    writable: true,
    enumerable: true,
    configurable: true
  },
  lastName: {
    value: 'Jeong',
    writable: false,
    enumerable: false,
    configurable: false
  }
}
//누락된 디스크립터 객체의 프로퍼티는 undefined나 false로 초기화된다.

//[[Writable]], [[Enumerable]], [[Configurable]]이 false

person.lastName = 'hihi';//무시된다. 에러는 x
console.log(Object.keys(person));//{"firstName"} 열거x
delete person.lastName;
//Uncaught TypeError: Cannot redefine property: lastName


//접근자 프로퍼티 정의

Object.defineProperty(person,'fullName', {
	get() {
		return `${this.firstName} ${this.lastName}`;
	},
	set(name) {
		[this.firstName, this.lastName] = name.split(' ');

	},
	enumerable: true,
	configurable: true
})

```

## 5. 객체 변경 방지

**객체는 변경 가능한 값이다**

객체는 재할당 없이 직접 변경할 수 있다.

- 프로퍼티 추가 및 삭제
- 프로퍼티 값 갱신
- 프로퍼티 어트리뷰트 재정의

**객체의 변경을 방지하는 방법**

자바스크립트는 객체의 변경을 방지하는 다양한 메서드를 제공한다. 메서드에 따라 그 범위가 다르다.

| 구분           | 메서드                   | 프로퍼티 추가 | 프로퍼티 삭제 | 프로퍼티 값 읽기 | 프로퍼티 값 쓰기 | 프로퍼티 어트리뷰트 재정의 |
| -------------- | ------------------------ | ------------- | ------------- | ---------------- | ---------------- | -------------------------- |
| 객체 확장 금지 | Object.preventExtensions | x             | o             | o                | o                | o                          |
| 객체 밀봉      | Object.seal              | x             | x             | o                | o                | x                          |
| 객체 동결      | Object.freeze            | x             | x             | o                | x                | x                          |

### 5.1 객체 확장 금지

**Object.preventExtensions**

Object.preventExtensions 메서드는 객체의 확장을 금지한다. 즉 프로퍼티 추가를 금지하는 것이다.

다음의 프로퍼티 추가 방법이 모두 금지된다.

- 프로퍼티 동적추가
- Object.defineProperty 를 통한 프로퍼티 추가 및 정의

확장 가능여부는 Object.isExtensible 메서드로 확인 가능하다.

### 5.2 객체 밀봉

**Object.seal**

Object.seal 메서드는 객체를 밀봉한다.

객체 밀봉(seal) 이란 다음을 금지한다.

- 프로퍼티 추가 및 삭제
- 프로퍼티 어트리뷰트 재정의 금지

기존 프로퍼티 값의 읽기, 갱신 이외에는 모두 불가하다.

객체의 밀봉여부는 Object.isSealed 메서드로 확인가능하다.

### 5.3 객체 동결

**Object.freeze**

Object.freeze 메서드는 객체를 동결한다.

객체 동결(freeze)는 다음을 금지한다.

- 프로퍼티 추가 및 삭제
- 프로퍼티 어트리뷰트 재정의 금지
- 프로퍼티 값 갱신

즉 동결된 객체는 프로퍼티 값 읽기만 가능하다.

객체의 동결여부는 Object.isFrozen 메서드로 확인가능하다.

### 5.4 불변 객체

**중첩 객체까지 동결하는 방법**

얕은 변경 방지(shallow only)가 아닌 중첩객체까지 동결된 불변객체(immutable object) 를 구현하려면,

객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 Object.freeze 메서드를 호출해야한다.

```
function deepFreeze(target) {
	if(target && typeof target === 'object' && !Object.isFrozen(target)) {
		Object.freeze(target);

		Object.keys(target).forEach(key => Object.deepFreeze(target[key]));
	}
	return target;
}
```
