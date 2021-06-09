---
title: Iterable
date: 2021-06-09 20:01:45
category: "javascript"
draft: false
---

# 이터러블

## 이터레이션 프로토콜

자바스크립트에는 다음과 같은 순회가능한 자료구조가 있다.

- 배열
- 문자열
- 유사배열객체
- DOM컬렉션
- 등등

위와 같은 자료구조들은 for in, for 문 등으로 순회 가능하다는 공통점이 있다.

그럼 자바스크립트 내부적으로 일정한 규약이 내부슬롯, 내부 메서드 등으로 정의되어 있을 것이라고 예상할 수 있다.

**But, ES5까지는?**통일된 규약 없이 각자의 방식으로 순회가능한 자료구조를 구현하였다.

**ES6에서는 규격이 일원화**

ES6부터 순회가능한 자료구조들이 **이터레이션 프로토콜**을 준수하는 **이터러블**로 통일되었다.

즉 이터레이션 프로토콜은 자료구조를 순회하기 위해 미리 약속된 규칙이라고 할 수 있다.

이터레이션 프로토콜의 종류로 두가지가 있다.

- 이터러블 프로토콜
- 이터레이터 프로토콜

**이터러블 프로토콜**

Symbol.iterator를 프로퍼티 키로 가진 메서드를 호출 하면 **이터레이터 프로토콜**을 준수한 이터레이터를 반환한다.

이러한 규약을 이터러블 프로토콜이라한다. 이터러블 프로토콜을 준수한 객체를 이터러블이라고 한다.

**이터레이터 프로토콜**

이터러블의 Symbol.iterator 메서드를 호출하면 이터레이터 프로토콜을 준수한 이터레이터를 반환한다.

**이터레이터는 next 메서드를 가지며 next 메서드를 호출하면 이터러블을 순회하며 value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환**한다. 이러한 규약을 이터레이터 프로토콜이라한다. 이터레이터 프로토콜을 준수한 객체를 이터레이터라고 한다.

즉 이터러블이 되기위해서는 다음과 같은 조건이 필요하다.

1. Symbol.iterator를 호출하여 이터레이터를 반환 (이터러블 프로토콜 )
2. next 메서드를 가지며 next 메서드를 호출하였을 때 value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환(이터레이터 프로토콜)

### 이터러블

이터러블 프로토콜을 준수한 객체이다. 이터러블은 Symbol.iterator를 키로 가진 메서드를 갖는데 이 메서드는 해당 객체에서 직접 구현될 수도 있고 프로토타입 체인을 통해 상속받을 수도 있다. 다음은 이터러블인지 확인하는 코드이다.

```js
const isIterable = v => !== null && typeof v[Symbol.iterator] === 'function'
```

**이터러블 예시**

- 문자열
- 배열
- Set
- Map

**프로토타입체인을 통해 Symbol.iterator를 상속받는 경우**

대표적인 자료구조로 array가 있다.

```js
Symbol.iterator in array; // true
```

특징

- for of 문으로 순회가능하다.
- 스프레드 문법 대상이 된다.
- 배열 디스트럭쳐링 할당의 대상으로 사용가능하다.

```js
const array = [0, 1, 2, 3];
// for of 문으로 순회 가능하다.
for (const item of array) {
  ("something");
}
// 스프레드 문법 대상이 된다.
[...array];
// 디스트럭쳐링 할당 대상이 된다.
const [a, ...rest] = array;
```

**일반 객체가 이터러블이 되려면**

이터러블 프로토콜을 준수해야한다. 즉 사용자 정의 이터러블을 직접 구현함으로서 이터러블을 생성할 수 있다.

### 이터레이터

Symbol.iterator를 호출했을 때 반환되는 객체가 이터레이터이다. 이터레이터 프로토콜을 준수한 이터레이터는 다음과 같은 특징을 갖는다.

- next 메서드 소유
- next 메서드를 호출 시 value 와 done 프로퍼티를 갖는 이터레이터 result 객체를 반환한다.
  - value는 순회중인 요소의 값, done은 이터러블의 순회 완료 여부를 나타낸다.

**이터레이터 예시**

```js
const arr = [0, 1, 2, 3];

const iterator = arr[Symbol.iterator]();

iterator.next(); // {value: 0, done: false}
iterator.next(); // {value: 1, done: false}
iterator.next(); // {value: 2, done: false}
iterator.next(); // {value: 3, done: true}
```

### 빌트인 이터러블

이터레이션 프로토콜을 준수한 객체인 빌트인 이터러블

- Array
- String
- Map
- Set
- arguments
- dom collection
- typedArray

### for of

**일반 loop으로 구현하면**

```js
const iterable = [1, 2, 3];

const iterator = iterable[Symbol.iterator]();

while (1) {
  //이터레이터는 next 메서드를 호출하며 d이터레이터 리절트 객체를 반환한다.
  const res = iterator.next();

  if (res.done) break;

  console.log(res.value);
}
```

**Array.prototype.forEach 메서드와의 비교**

- for of 문은 break, continue, return 문을 사용할 수 있다.

### 유사배열객체

인덱스로 요소에 접근할 수 있고, length 프로퍼티를 가지는 객체를 유사배열객체라고 한다. 단 모든 유사배열객체가 이터러블은 아니다.

유사배열객체이면서 이터러블인 객체는 다음과 같다.

- arguments
- NodeList
- HTMLCollection
- 배열

### 이터레이션 프로토콜의 필요성

자바스크립트의 순회가능한 자료구조들이 모두 각각의 구현방식을 가지고 있다면 해당 자료구조를 이용하는 문법들에게 각각의 구현방식을 적용해야한다.

이는 하나로 통일했을 때보다 비효율적이다.

이터레이션 프로토콜은 자료구조들에 하나의 순회방식을 갖도록 규정하여 효율적으로 자료구조들을 사용할 수 있도록 한다.

### 사용자 정의 이터러블
