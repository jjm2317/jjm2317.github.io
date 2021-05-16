---
title: javascript Spread
date: 2020-10-22 16:13:32
category: "javascript"
draft: false
---

# 스프레드 문법

```
console.log(... [1, 2, 3]); //1 2 3

console.log(...'Hello'); // H e l l o

console.log(...new Map([['a', '1'], ['b', '2']]))// ['a', '1'] ['b', '2']
console.log(...new Set([1, 2, 3])); //1 2 3

console.log(...{a: 1, b: 2});
// TypeError
```

```
const list = ...[1, 2, 3]; //SyntaxError
```

## 1. 함수 호출문의 인수 목록에서 사용하는 경우

```
const arr = [1, 2, 3];
const max = Math.max(arr); //NaN
```

```
Math.max(1); //1
Math.max(1, 2); //2
Math.max(1, 2, 3); //3
Math.max(); //-Infinity

Math.max([1,2,3]); //NaN
```

```
var arr = [1, 2, 3];

var max = Math.max.apply(null, arr); //3
```

```
const max = Math.max(...arr)
```

```
//Rest 파라미터

function foo(...rest) {
	console.log(rest);
}

foo(...[1, 2, 3]);
```

## 2. 배열 리터럴 내부에서 사용하는 경우

### concat

```
var arr = [1, 2].concat([3, 4]);
console.log(arr); //[1, 2, 3, 4]
```

```
const arr= [...[1, 2], ...[3, 4]];
console.log(arr); //[1, 2, 3, 4]
```

### splice

```
var arr1 = [1,4];
var arr2 = [2, 3];

arr1.splice(1, 0, arr2);

console.log(arr1); //[1,[2, 3], 4]
```

```
var arr1= [1, 4];
var arr2 = [2, 3];

Array.prototype.splice.apply(arr1, [1, 0].concat(arr2));
console.log(arr1);
```

```
const arr1 = [1, 4];
const arr2 = [2, 3];

arr1.splice(1, 0, ...arr2);
console.log(arr1); //[1, 2, 3, 4]
```

### 배열 복사

```
var origin = [1, 2];
var copy = origin.slice();

console.log(copy);
console.log(copy === origin); //false
```

```
const origin = [1, 2];
const copy = [...origin];

console.log(copy); [1, 2]
console.log(copy === origin); //false
```

### 이터러블을 배열로 변환

```
function sum() {
	var args = Array.prototype.slice.call(arguments);

	return args.reduce(function (pre, cur){
		return pre + cur;
	}, 0);
}

console.log(sum(1, 2, 3)); // 6
```

```
const arrayLike = {
	0: 1,
	1: 2,
	2: 3,
	length: 3
};

const arr = Array.prototype.slice.call(arrayLike); //[1, 2, 3]
console.log(Array.isArray(arr));
```

```
function sum() {
	return [...arguments].reduce((pre, cur) => pre + cur, 0);
}

console.log(sum(1, 2, 3)); // 6
```

```
const sum = (...args) => args.reduce((pre, cur) => pre + cur, 0);

console.log(sum(1, 2, 3));
```

```
const arrayLike = {
	0: 1,
	1: 2,
	2: 3,
	length: 3
};

const arr = [...arrayLike]
//TypeError
```

```
Array.from(arrayLike); // [1, 2, 3]
```

### 객체 리터럴 내부에서 사용하는 경우

```
const obj = { x: 1, y: 2};
const copy = {...obj};
console.log(copy); //{x: 1, y: 2}
console.log(obj === copy); //false

const merged = {x: 1, y: 2, ...{a: 3, b: 4}};
console.log(merged); // {x: 1, y: 2, a: 3, b: 4}
```

```
const merged = Object.assign({}, {x: 1, y: 2}, {y: 10, z: 3});
console.log(merged)l //{x: 1, y: 10, z: 3}

const changed = Object.assign({}, {x: 1, y: 2}, {y: 100});
console.log(changed); //{x: 1, y: 100}

const added = Object.assigin({}, {x: 1, y: 2}, {z: 0});
console.log(added); // {x: 1, y: 2, z: 0}
```

```
const merged = {...{x: 1, y: 2}, ...{y: 10, z: 3}};
console.log(merged); //{x: 1, y: 10, z: 3}

const changed = {...{x: 1, y: 2}, y: 100};

console.log(changed); //{x: 1, y: 100}

const added = {...{x: 1, y: 2}, z: 0};

console.log(added); //{x: 1, y: 2, z: 0}
```
