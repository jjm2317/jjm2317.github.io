---
title: Generator
date: 2021-06-10 01:31:10
category: "javascript"
draft: false
---

# 제네레이터

제네레이터는 한번 호출되면 함수 코드를 일괄 실행하는 일반함수와 달리, 코드블록의 실행을 중단 했단가 필요한 시점에 재개할 수 있는 함수다.

제네레이터 함수의 특징은 다음과 같다.

1. 함수 호출자(caller 프로퍼티에 바인딩된 객체)가 함수 실행을 제어할 수 있다.
2. 입력 값과 반환 값만 존재하는 일반함수와 달리, 제네레이터는 함수 호출자가 함수 코드 실행 중간에 상태를 주고 받을 수 있다.
3. 제네레이터 함수를 호출 시 제네레이터 객체를 반환한다. 제네레이터 객체는 이터러블이면서 이터레이터이다.

## 제네레이터 함수 정의 방법

```js
// 함수 선언문
function* gen1() {
  yield 1;
}
// 함수 표현식
const gen2 = (function* () {
  yield 1;
})(
  // 메서드
  {
    *gen3() {
      yield 1;
    },
  }
);
```

- (\*) 는 애스터리스크라고 한다.
- 제네레이터는 화살표 함수로 정의할 수 없다.
- [[Construct]] 내부 메서드를 호출 할 수 없는 non-constructor이다.

## 제네레이터 객체

제네레이터 함수를 호출하면 제네레이터 객체를 반환한다.

제네레이터 객체는 이터러블이며 이터레이터이다.

- Symbol.iterator 메서드를 소유하거나 상속받았다.
- next 메서드를 호출하여 이터레이터 객체를 반환한다.
- 이터레이터와의 차이점
  - return, throw 메서드를 가진다.

```js
function* gen() {
  console.log("start");
  yield 1;
  yield 2;
  yield 3;
}

const generator = gen();

//next 메서드 호출 시 다음 yield 문 까지 실행하고 value 프로퍼티를 yield 값으로 받는 이터레이터 리절트 객체를 반환한다.
console.log(generator.next());
/*
start
{value: 1, done: false}
*/

// return 메서드를 호출 시 인수로 전달한 값을 value로, done프로퍼티를 true를 가지는 이터레이터 리절트 객체를 반환한다.
```

## 제네레이터의 일시 중지와 재개

- 제네레이터 객체의 next 메서드를 호출 하면 yield 표현식 까지 실행되고 일시 중지 된다.
  - 함수의 제어권이 호출자(caller)로 양도(yield) 된다.

**제네레이터 객체의 next 메서드에는 인수를 전달할 수 있다.**

전달한 인수는 제네레이터 함수코드에서 yield 표현식을 할당받는 변수에 할당된다.

```js
function* gen() {
  const x = yield 1;
  const y = yield x + 10;
  return x + y;
}
const generator = gen();

//첫번째 next 메서드의 인수로는 인수를 전달하지 않으며 전달하더라도 무시된다.
console.log(generator.next());
//두번째  next 메서드의 인수로 전달된 값은 x 에 할당된다.
console.log(generator.next(3));
//세번째 next 메서드의 인수로 전달된 값은 y값에 할당된다.
console.log(generator.next(1));
/*
{ value: 1, done: false }
{ value: 13, done: false }
{ value: 4, done: true }
*/
```

- next 메서드의 yield 표현식을 통해서 제네레이터함수는 호출자와 상태를 주고받을 수 있다.

- 제네레이터 함수를 이용하여 비동기 처리를 동기처럼 구현할 수 있다.

## 활용

### 이터러블 구현

이터레이션 프로토콜로 직접 구현하는 것보다 쉽게 이터러블을 구현할 수 있다.

**이터레이션 프로토콜을 준수하는 무한피보나치 수열**

```js
const infiFibo = function () {
  let [pre, cur] = [0, 1];

  return {
    [Symbol.iterator]() {
      return this;
    },
    next() {
      [pre, cur] = [cur, pre + cur];
      return { value: cur };
    },
  };
};

const iterable = infiFibo();

const result = [];
for (let value of iterable) {
  if (value > 100) break;
  result.push(value);
}
```

**제네레이터 함수를 이용한 이터러블 구현**

```js
const infiFibo = (function* () {
    let [pre, cur] = [0, 1];

    while(true) {
        [pre, cur] = [cur, pre + cur]
        yield cur;
    }
})())
```

### 비동기 처리

프로미스의 후속 처리 메서드 then / catch / finally 없이 비동기 처리 결과를 반환하도록 구현 가능하다.

```js
const async = (gen) => {
  const generator = gen();

  const onResolved = (arg) => {
    const result = generator.next(arg);
    console.log(result);
    return result.done
      ? result.value
      : result.value.then((res) => onResolved(res));
  };

  return onResolved;
};
async(function* fetchTodo() {
  const url = "https://jsonplaceholder.typicode.com/todos/1";

  const response = yield fetch(url);
  const todo = yield response.json();
  console.log(todo);
})();
```

yield 표현식은 pending 상태의 promise를 그대로 반환한다.
