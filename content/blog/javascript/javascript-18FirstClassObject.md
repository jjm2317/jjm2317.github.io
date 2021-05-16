---
title: javascript 18FirstClassObject
date: 2020-09-25 11:28:15
category: "javascript"
draft: false
---

# 함수와 일급 객체

## 1. 일급 객체

**일급 객체의 조건**

다음과 같은 조건을 만족하는 객체를 일급 객체(first-class object)라한다

- 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성가능하다
- 변수나 자료구조(객체, 배열 등) 에 저장할 수 있다
- 함수의 매개변수에게 전달할 수 있다.
- 함수의 반환값으로 사용할 수 있다.

**함수는 일급 객체이다**

자바스크립트의 함수는 위의 조건을 모두 만족하므로 일급 객체이다.

```

```

## 2. 함수 객체의 프로퍼티

**함수는 프로퍼티를 가질 수 있다**

함수는 객체이다. 따라서 함수도 프로퍼티를 가질 수 있다. 브라우저 콘솔에서 console.dir 메서드 실행하면 프로퍼티가 내부에 존재하는 것을 알 수 있다.]

**함수의 프로퍼티의 프로퍼티어트리뷰트**

함수의 프로퍼티에 대해 Object.getOwnPropertyDescriptors 메서드로 확인해보면 다음의 프로퍼티가 존재한다

- 데이터 프로퍼티
  - arguments, caller, length, name, prototype
  - 일반 객체에는 없는 함수객체 고유의 프로퍼티
- 접근자 프로퍼티
  - `__proto__`
    - Object.prototype 객체의 프로퍼티를 상속받았다
    - 모든 객체가 사용할 수 있다

### 2.1 arguments 프로퍼티

**arguments의 프로퍼티 값**

함수 객체의 arguments 프로퍼티 값은 arguments 객체다. arguments 객체는 함수 호출 시 전달된 인수(argument)들의 정보를 담고 있는 순회 가능한(iterable) 유사 배열 객체이며, 함수 내부에서 지역변수처럼 사용된다. 함수외부에서는 참조할 수 없다.

**권장 사용법**

arguments 프로퍼티는 ES3 부터 표준에서 폐지되었다.

Function.arguments와 같은 사용법은 권장되지 않으며 함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체를 참조하도록 하자

**arguments 객체의 기능**

함수를 정의할 때 선언한 매개변수는 함수 몸체 내부에서 변수와 동일하게 취급된다. 즉, 함수가 호출되면 함수 몸체 내에서 암묵적으로 매개변수가 선언되고 undefined로 초기화된 이후 인수가 할당된다.

선언된 매개변수의 개수보다 인수를 적게 전달했을 경우 인수가 전달되지 않은 매개변수는 undefined로 초기화된 상태를 유지한다. 매개변수의 개수보다 인수를 더 많이 전달한 경우 초과된 인수는 arguments 객체의 프로퍼티로 보관된다

arguments 객체는 인수를 프로퍼티 값으로 소유하며 프로퍼티 키는 인수의 순서를 나타낸다. arguents 객체의 callee 프로퍼티는 호출되어 arguments 객체를 생성한 함수, 즉 함수 자신을 가리키고 argumnets 객체의 length 프로퍼티는 인수의 개수를 가리킨다.

**arguments 객체의 Symbol(Symbol.iterator)프로퍼티**

arguments 객체의 Symbol 프로퍼티는 arguments 객체를 순회 가능한 자료구조인 iterable 로 만들기 위한 프로퍼티다. Symbol.iteraotr를 프로퍼티 키로 사용한 메서드를 구현하는 것에 의해 이터러블이 된다.

```
function multiply(x,y ){
	//이터레이터
	const iterator = argumnts[Symbol.iterator]();

	//이터레이터의 next 메서드를 호출하여 이터러블 객체 arguments를 순회
	console.log(iterator.next());// value: 1
	console.log(iterator.next());// value: 2

	return x * y;
}
multiply(1,2,3);
```

**arguments 객체를 통한 가변인자 함수 구현**

선언된 매개변수의 개수와 함수를 호출할 때 전달하는 인수의 개수를 확인하지 않는 자바스크립트의 특성 때문에 함수가 호출되면 인수 개수를 확인하고 이에 따라 함수의 동작을 달리 정의할 필요가 있을 수 있다. 이때 유용하게 사용되는 것이 arguments 객체다.

arguments 객체는 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 사용된다.

```
function multiply(){
	let res = 1;
	for(let i = 0; i < arguments.length; i++){
		res *= arguments[i];
	}

	return res;
}

console.log(multiply());//1
console.log(multiply(1,2,6)); //12
```

**arguments 객체는 유사배열 객체이다.**

arguments 객체는 배열 형태로 인자 정보를 담고 있지만 실제 배열이 아닌 유사 배열 객체 (array- like-object)다. 유사 배열 객체란 length 프로퍼티를 가진 객체로 for 문으로 순회가능한 객체를 말한다.

**유사 배열 객체와 이터러블**

ES6에서 도입된 이터레이션 프로토콜을 준수하면 순회가능한 자료구조인 이터러블이 된다. 이터러블의 개념이 없었던 ES5에서 arguments 객체는 유사배열객체로 구분되었다. 하지만 이터러블이 도입된 ES6부터 arguments 객체는 유사 배열 객체이면서 동시에 이터러블이다.

**유사 배열 객체의 특징**

유사 배열 객체는 배열이 아니므로 배열 메서드를 사용할 경우 에러가 발생한다. 따라서 배열 메서드를 사용하려면 Function.prototype.call, Function.prototype.apply 를 사용해 간접 호출해야하는 번거로움이 있다.

```
function multiply(){
	const array = Array.prototype.slice.call(arguments);
	return array.reduce(function (pre, cur) {
		return pre * cur;
	}, 1);
}

console.log(multiply());//1
console.log(multiply(1,2,6)); //12
```

**ES6의 Rest 파라미터**

```
function multiply(...args){
	return args.reduce((pre, cur) => pre * cur, 1);
}
console.log(multiply(3,5,6));//90
```

### 2.2 caller 프로퍼티

**caller 프로퍼티의 값**

caller 프로퍼티는 ECMAScript 사양에 포함되지 않은 비표준 프로퍼티다. 이후 표준화될 예정도 없는 프로퍼티이므로 참고로만 알아두자.

함수객체의 caller 프로퍼티는 함수 자신을 호출한 함수를 가리킨다.

```
function foo(func) {
	return func();
}

function bar() {
	return 'caller: ' + bar.caller;
}


console.log(foo(bar));//caller: function foo(func) {
	return func();
}

console.log(bar());
```

### 2.3 length 프로퍼티

함수 객체의 length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다.

### 2.4 name 프로퍼티

함수 객체의 name 프로퍼티는 함수 이름을 나타낸다 ES6부터 정식 표준이다.

익명함수 표현식에서, ES5에서는 빈문자열을 반환했지만, ES6에서는 함수객체를 가리키는 식별자를 반환한다.

### 2.5 `__proto__`접근자 프로퍼티

모든 객체는 [[Prototype]]이라는 내부 슬롯을 갖는다. [[Prototype] ]내부슬롯은 객체 지향 프로그래밍의 상속을 구현하는 프로토타입 객체를 가리킨다.

`__proto__`접근자 프로퍼티는 [[Prototype]]내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티다.

### 2.6 prototype 프로퍼티

prototype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체, 즉 constructor 만이 소유하는 프로퍼티다. 일반 객체와 생성자 함수로 호출할 수 없는 non-constructor 에는 prototype 프로퍼티가 없다.
