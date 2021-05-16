---
title: javascript Symbol
date: 2021-04-24 12:34:42
category: "javascript"
draft: false
---

# Symbol

## Symbol 이란?

Symbol은 데이터 타입이다.

ES6에서 **Symbol 데이터 타입**이 새로 추가되어 자바스크립트의 데이터 타입은 다음과 같은 7가지가 되었다.

- String
- Number
- Boolean
- undefined
- null
- object
- Symbol

**Symbol의 특징**

- 원시값으로 불변 값이다.
- 다른값과 중복되지 않는 유일한 값이다.

**사용하는 이유**

- 이름 충돌위험이 없는 유일한 **프로퍼티 키**를 만들기 위해 사용한다.

- 상수를 구현할 때 사용된다.

## Symbol 값의 생성

Symbol 값을 생성하는 방법은 다음과 같다

- Symbol 함수
- Symbol.for
- Symbol.keyFor

### Symbol 함수

Symbol값은 다른 원시값들과 다르게 Symbol 함수를 호출하여야만 생성할 수 있다.

```js
//생성된 심벌 값은 외부에서 확인 할 수 없다.
const mySymbol = Symbol();

console.log(mySymbol); // Symbol()

//심벌 함수는 생성자가 아니다.
new Symbol(); // TypeError
```

**Symbol 함수의 인수**

Symbol 함수는 문자열을 인수로 받을 수 있다. 단 해당 값은 description의 용도로만 사용된다.

즉, 같은 description 을 전달한 심벌 값 두개는 다른 값이다.

```js
const firstSymbol = Symbol("first");
const secondSymbol = Symbol("second");

firstSymbol === secondSymbol; // false
```

**래퍼 객체 생성**

심벌값은 원시값이지만 Symbol.prototype의 프로퍼티를 사용하여 접근하면 래퍼객체를 생성한다.

(참고) 래퍼 객체를 생성하는 원시값

- String
- Number
- Boolean

Symbol.prototype의 프로퍼티 description, toString()

```js
const mySymbol = Symbol("hello");

mySymbol.description; // hello
mySymbol.toString(); //mySymbol(hello)
```

**Symbol 값의 타입변환**

- 문자열이나 숫자값으로 암묵적 타입변환이 일어나지 않는다
- 불리언 값으로는 암묵적 타입변환이 일어난다.

### Symbol.for / Symbol.keyFor

**Symbol.for 과 Symbol 함수와의 차이점**

심벌값들이 관리되는 전역 심벌 레지스트리가 있다.

위의 Symbol함수를 통한 심벌값의 경우에는 전역 심벌 레지스트리에 저장되지 않을뿐더러, 심벌 레지스트리에서 해당 심벌값을 찾을 수 있는 키를 지정할 수 있는 방법도 없다.

이에 반해 Symbol.for 함수는 **인수로 키를 전달**하여 생성된 **심벌 값을 전역 심벌 레지스트리에 저장하거나 조회**한다. 키에 해당하는 값이 없으면 심벌값을 생성하고, 존재하면 조회한다.

- Symbol.for 함수의 인수로 전달한 키에 해당하는 심벌값이 심벌 레지스트리에 없는 경우

```js
const mySymbol = Symbol.for("hello"); // 심벌 레지스트리에 hello를 키로 가진 심벌값이 없으므로 심벌 값을 생성한다.
const mySymbol2 = Symbol.for("hello"); //심벌레지스트리에 hello를 키로 가진 심벌 값이 위에서 생성되어 존재하므로 해당 값을 반환한다.
mySymbol === mySymbol2; // true
```

**Symbol.keyFor**

심벌값을 저장한 변수를 인수로 전달하면 해당 심벌값의 키를 반환한다.

```js
const mySymbol = Symbol.for("hello"); //hello를 키로하여 심볼값 생성
Symbol.keyFor(mySymbol); //hello,  mySymbol 변수에 저장된 심벌값의 키를 반환
```

## Symbol 사용 예시

### 상수 구현

react_prac 레포의 컴포넌트를 조건부 렌더링을 한다고 가정했을때 출력모드를 설정해보자

**원시값을 통한 상수 구현**

```js
const RenderModes = {
  COUNTER: "counter",
  USER: "user",
  ALL: "all",
};

/*some codes(출력 모드에따른 렌더링)*/
```

상수 이름에 할당된 값은 **다른 값들과 중복될 가능성**이 있고 **변경될 가능성**도 있다.

**심벌을 통한 상수 구현**

```js
const RenderModes = {
  COUNTER: Symbol.for("counter"),
  USER: Symbol.for("user"),
  ALL: Symbol.for("all"),
};
```

다른 값들과 **중복될 가능성이 없다**

**Object.freeze를 통한 enum 구현**

enum은 숫자 상수의 집합이다.

```js
const RenderModes = Object.freeze({
  COUNTER: Symbol.for("counter"),
  USER: Symbol.for("user"),
  ALL: Symbol.for("all"),
});
```

위 객체는 **변경될 가능성이 없다.**

### 유일한 프로퍼티 키 생성

**Symbol로 프로퍼티 만드는법**

- Symbol값을 대괄호로 묶어서 프로퍼티키에 사용한다.
- 프로퍼티 값 참조시, 마찬가지로 대괄호 접근연산자로 참조한다.

```js
const obj = {
  [Symbol.for("myKey")]: "hello",
};

obj[Symbol.for("myKey")]; //hello
```

**다른 프로퍼티 키와 충돌할 위험이 없다.**

**프로퍼티 은닉 효과**

```js
//위 코드
for (const key in obj) {
  console.log(key); // none
}
Object.keys(obj); //[]
Object.getOwnPropertyNames(obj); // []

//찾는법
Object.getOwnPropertySymbols(obj); // Symbol(myKey)
```

for in 문, Object.keys 메서드, Object.getOwnPropertyNames 메서드로 찾을 수 없다.

프로퍼티 은닉효과를 이용해서 만약 표준 빌트인 객체를 확장할 필요가 있는 경우 Symbol을 통해 확장할 수 있다.

## Well-known Symbol, Symbol.iterator

자바스크립트가 기본으로 제공하는 Symbol 값이 있다. 이 Symbol 값은 Symbol 함수의 프로퍼티로 저장되어 있다.

이러한 built-in Symbol 값을 Well-known Symbol이라고 한다.

대표적인 것으론 **Symbol.iterator** 메서드가 있다.

이 메서드는 **이터러블**을 구현하는데 사용된다.

(참고) 이터러블 종류

- String, Array, Map, Set, arguments, NodeList 등

이터러블은 Symbol.iterator 메서드를 가진다.

**Symbol.iterator는 호출되어 iterator를 반환한다.**

빌트인 이터러블은 이러한 과정을 이터레이션 프로토콜로서 준수한다.

일반객체가 이터레이션 프로토콜을 준수하게되면 이터러블이 된다.

**일반 객체를 이터러블로 만드는 방법**

```js
const iterable = {
  [Symbol.iterator]() {
    return {
      next() {
        return { value: cur++, done: cur > max + 1 };
      },
    };
  },
};
```
