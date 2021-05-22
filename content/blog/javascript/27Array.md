---
title: 27Array
date: 2020-10-21 18:36:12
category: "javascript"
draft: false
---

# 배열

- 동일한 메모리공간을 연속적으로 확보한다.

- random access가빠르다 O(1);
- 유사배열객체와는 속도의 차이가 있다.

- 자료구조 사용이유
  - 관련있는 것들끼리 모으기 위해
- 배열을 만들때 요소의 타입이 갖도록 해야한다.
  - 최적화가 일어나기 때문

## 배열 메서드



### Array.isArray

```
//true
Array.isArray([]); //true
Array.isArray([1,2]);
Array.isArray(new Array());

//false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(1);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray({0 : 1, length: 1})
```



### Array.prototype.indexOf

```
const arr = [1,2,3,4];

arr.indexOf(2); //1
arr.indexOf(4); //-1
arr.indexOf(2,2);//2
```

```
const foods = ['apple', 'banana', 'orange'];

if (foods.indexOf('orange') === -1) {
	foods.push('orange');
}

console.log(foods);
```

```

```



### Array.prototype.push

```
const arr = [1,2];

let result = arr.push(3, 4);
console.log(result);//4

console.log(arr); // [1, 2, 3, 4];
```

```
const arr = [1, 2];

arr[arr.length] = 3;
console.log(arr); // [1, 2, 3]
```

```
const arr = [1, 2];

const newArr = [...arr, 3];
console.log(newArr); // [1, 2, 3]
```



### Array.prototype.pop

```
const arr = [1, 2];

let result = arr.pop();
console.log(result); //2

console.log(arr); //[1]
```

```
const Stack = (function () {
	function Stack(array = []) {
		if (!Array.isArray(array)){
			throw new TypeError(`${array} is not an array.`);
		}
		this.array = arrayp
	}
	
	Stack.prototype = {
		constructor: Stack,
		
		push(value) {
			return this.array.push(value);
		},
		
		pop() {
			return this.array.pop();
		},
		
		entries() {
			return [... this.array]
		}
	};
	
	return Stack
}());

const Stack = new Stack ([1, 2]);
console.log(stack.entries()); // [1, 2]

stack.push(3);
console.log(stack.entries()); // [1, 2, 3]

stack.pop();
console.log(stack.entries()); // [1, 2]
```

```
class Stack {
	#array; // private class member
	
	constructor(array = []) {
		if (!Array.isArray(array)) {
			throw new TypeError(`${array} is not an array.`);
		}
		this.#array = array;
	}
	
	push(value) {
		return this.#array.push(value);
	}
	
	pop() {
		return this.#array.pop();
	}
	
	entries() {
		return [...this.#array];
	}
}


```



### Array.prototype.unshift

```
const arr = [1, 2];

let result = arr.unshift(3, 4);

console.log(result); //4

console.log(arr); // [3, 4, 1, 2]
```

```
const arr = [1, 2];

const newArr = [3, ...arr];
console.log(newArr); // [3, 1, 2]
```

```
const arr1 = [1, 2];
console.log(arr1.unshift(3));//3
console.log(arr1);// [3, 1, 2]

arr1.unshift([1, 2]);
console.log(arr1); //[ [ 1, 2 ], 3, 1, 2 ] 전달 받은 배열을 그대로 저장

const arr2 = [1, 2];
arr2.unshift([3, 4], 1);
console.log(arr2); //[ [ 3, 4 ], 1, 1, 2 ] 숫자 배열 혼합도 그대로 저장

```



### 8.6 Array.prototype.shift

```
const arr = [1, 2];

let result = arr.shift();
console.log(result); // 1

console.log(arr); // [2]
```





```
// 큐 생성자 함수
const Queue = (function () {
	function Queue(array = []) {
		this.array = array;
	}
	Queue.prototype = {
		constructor: Queue,
		
		enqueue(element) {
			this.array.push(element);
		}
		dequeue(element) {
			this.array.shift();
		}
		
		entries(){
			return [...this.array];
		}
	}
	return Queue;
	
}());
```

```
// 큐 클래스
class Queue {
	#array;
	
	constructor(array = []) {
		if(!(array instanceof Array)) {
			throw new TypeError(`${array} is not array`);
		}
		this.#array = array;
	}
	
	enqueue (element) {
		this.#array.push(element);
	}
	
	dequeue () {
		this.#array.shift();
	}
	entries() {
		return [...this.aray];
	}
	
	return Queue;
}
```





### Array.prototype.concat

```
const arr1 = [1, 2];
const arr2 = [3, 4];

let result = arr.concat(arr2);
console.log(result); [1, 2, 3, 4]

result = arr1.concat(3);
console.log(result); // [1, 2, 3]

result = arr1.concat(arr2, 5);
console.log(result); //[1, 2, 3, 4, 5]

consol.log(arr1); // [1, 2]


const arr1 = [1, 2, 3];

const arr2 = arr1.concat(1,2,3);

console.log(arr2);//[ 1, 2, 3, 1, 2, 3 ]
console.log(arr1);//[ 1, 2, 3 ] 원본 배열 안 변한다.

console.log(arr1.concat([1,2]));//[ 1, 2, 3, 1, 2 ] //배열 인수도 가능
console.log([1, 2].concat(arr1, 3));//[ 1, 2, 1, 2, 3, 3 ] 배열과 숫자 혼합 가능
```

```
const arr1 = [3, 4];

arr.unshift(1, 2);

console.log(arr1); // [1,2,3,4]

arr1.push(5, 6);

console.log(arr1); // [1, 2, 3, 4, 5, 6]

const arr2 = [3, 4];

let result = [1, 2].concat(arr2);

console.log(result); //[1, 2, 3, 4]

result = result.concat(5, 6);
console.log(result); // [1, 2, 3, 4, 5, 6]
```



```
//Array.prototype.concat 메서드 스프레드 문법 대체
const arr1 = [1, 2];

let result = [0, ...arr1, 3, 4];
console.log(result); // [0, 1, 2, 3, 4]

result = [...result, ...[5, 6]];

console.log(result); // [0, 1, 2, 3, 4, 5, 6]
```



### Array.prototype.splice

```
const arr = [1, 2, 3, 4];

const result = arr.splice(1, 2, 20, 30);

console.log(result); // [2, 3]

console.log(arr);[1, 20, 30, 4]
```



```
const arr1 = [1, 2, 3];

console.log(arr1.splice(1,1,1)); // [2] 제거한 요소를 배열로 반환
console.log(arr1); // [ 1, 1, 3 ] 원본 배열 직접 변경

arr1.splice(1,0, [3,4]);
console.log(arr1); //[ 1, [ 3, 4 ], 1, 3 ] 배열 요소 전달시 그대로 저장

```



```
// 특정 요소 모두 제거
function remove(arr, item) {
  if(!(Array.isArray(arr))) {
    throw new TypeError(`${arr} is not array`);
  }
  let index = arr.indexOf(item);

  if(!(index === -1)) {
    arr.splice(index, 1);
    return remove(arr, item);
  }

  return arr;
}

console.log(remove([1, 2, 3, 2, 4, 5, 2], 2)); // [1, 3, 4, 5]
```



### Array.prototype.slice

```

```



### Array.prototype.join

```
const arr = [1, 2, 3, 4];

arr.join(); // 1, 2, 3, 4

console.log(arr);
//[1, 2, 3, 4]
```



### Array.prototype.reverse

```
const arr = [1, 2, 3];

const result = arr.reverse();

console.log(arr); [3, 2, 1];
console.log(result); [3, 2, 1]
```





### Array.prototype.fill

```
const arr = [1, 2, 3];

const res = arr.fill(0);

console.log(arr); // [0, 0, 0]
```

```
const arr = [1, 2, 3];

arr.fill(0, 1);

console.log(arr); // [1, 0, 0]
```







```
const todos = [
	{ id: 4, content: 'JavaScript'},
	{ id: 1, content: 'HTML'},
	{ id: 2, content: 'CSS'}
];

function compare(key) {
	return (a, b) => (a[key] > b[key] ? 1 : (a[key] > b[key] ? -1 : 0));
}

todos.sort(compare('content'));
console.log(todos);

todos.sort(compare('content'));
console.log(todos);
```



### Array.prototype.forEach

```
const numbers = [1, 2, 3];
let pows = [];

for(let i = 0; i < numbers.length; i++) {
	pows.push(numbers[i] ** 2);
}
console.log(pows); [1, 4, 9]
```



```
const numbers = [1, 2, 3];
let pows = [];

numbers.forEach(item => pows.push(item ** 2));
console.log(pows);
```



```
[1, 2, 3].forEach((item, index, arr) => {
	console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
});
```

```
const numbers = [1, 2, 3];

numbers.forEach((item, index, arr) => { arr[index] = item ** 2;});
console.log(numbers);
```



```
class Numbers {
	numberArray = [];
	
	multiply(arr) {
		arr.forEach(function (item){
			this.numberArray.push(item * item);
		}); //TypeError
	}
}

const numbers = new Numbers();
numbers.multiply([1, 2, 3]);
```



### Array.prototype.map

```
const numbers = [1, 4, 9];

const roots = numbers.map(item => Math.sqrt(item));

console.log(roots);

console.log(numbers);
```

```
[1, 2, 3].map((item, index, arr) => {
	console.log(`item, index, JSON.stringify(arr)`);
	return item;
});
```

```
class Prefixer {
	constructor(prefix) {
		this.prefix = prefix;
	}
	
	add(arr) {
		return arr.map(function (item) {
			return this.prefix + item;
		}, this);
	}
}

const prefixer = new Prefixer('-webkit-');
console.log(prefixer.add(['transition', 'user-select']));
```

```
class Prefixer {
	constructor(prefix) {
		this.prefix = prefix;
	}
	
	add(arr) {
		arr.map((item) => this.prefix + item);
	}
}
```

### Array.prototype.filter

```
const numbers = [1, 2, 3, 4, 5];

const odds = numbers.filter(item => item % 2);

console.log(odds);
```

```
[1, 2, 3].filter((item, index, arr) => {
	console.log(`${item, index, JSON.stringify(arr)}`);
	return item % 2;
});
```

```
class Users {
	constructor() {
		this.users = [
			{ id: 1, name: 'Lee'},
			{ id: 2, name: 'Kim'}
		];
	}
	
	findById(id) {
		return this.users.filter(user => user.id === id);
	}
	
	remove(id) {
		this.users = this.user.filter(user.id !== id)
	}
}


```



### Array.prototype.reduce

```
const sum = [1, 2, 3, 4].reduce((accumulator, currentValue, index, array) => accumulator + currentValue, 0);

console.log(sum); //10
```



```
const values = [1, 2, 3, 4, 5, 6];

const average = values.reduce((acc, cur, i, { length}) => {
	return i === length - 1 ? (acc + cur) / length : acc + cur;
}, 0);

console.log(average);
```

```
const values = [1, 2, 3, 4, 5];

const max = values.reduce((acc, cur) => (acc > cur ? acc : cur), 0);

console.log(max);
```

```
const values = [1, 2, 3, 4, 5];

const max = Math.max(...values);

console.log(max);
```

```
const fruits = ['banana', 'apple', 'orange', 'orange', 'apple'];

const count = fruits.reduce((acc, cur) => {
	acc[cur] = (acc[cur] || 0) + 1;
	return acc;
}, {});

console.log(count);
```

```
const values = [1, [2, 3], 4, [5, 6]];
const flatten = values.reduce((acc, cur) => acc.concat(cur), []);
console.log(flatten);
```

```
[1, [2, 3], 4, [5, 6]].flat();



```

```
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];

const result = [... Set(values)];
console.log
```

```
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];

const result = values.filter((acc, cur, i, arr) => {})
```



```
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];

const result = values.reduce((acc, cur, i, arr) => {
	if (arr.indexOf(cur) === i)
})
```





### Array.prototype.map

```
const numbers = [1, 4, 9]

const roots = numbers.map(item => Math.sqrt(item));

console.log(roots);
// [1, 2, 3]

console.log(numbers); [1, 4, 9]
```

```
[1, 2, 3].map((item,index, arr) => {
	console.log(`${item, index, JSON.stringify(arr)}`);
	return item;
})
```

```
class Prefixer {
	constructor(prefix) {
		this.prefix = prefix;
	}
	
	add(arr) {
		return arr.map(item => this.prefix + item);
	}
}
```





### Array.prototype.filter

```
const numbers = [1, 2, 3, 4, 5];

const odds = numbers.filter(item => item % 2);
console.log(odds);
```

```
[1, 2, 3].filter((item, index, arr) => {
	return item %2;
})
```



```
class Users {
	constructor() {
		this.users = [
			{id : 1, name: 'Lee'},
			{id : 2, name: 'Kim'}
		];
	}
	
	findById(id) {
		return this.users.filter(item => item.id === id);
	}
	
	remove(id) {
		this.users = this.users.filter(item => item.id !== id);
	}
	
}
```





