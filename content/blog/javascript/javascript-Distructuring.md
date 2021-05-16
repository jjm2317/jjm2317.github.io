---
title: javascript Distructuring
date: 2020-10-22 16:45:14
category: "javascript"
draft: false
---

# 디스트럭처링 할당

## 1. 배열 디스트럭처링 할당

```
var arr = [1, 2, 3];

var one = arr[0];
var two = arr[1];
var three = arr[2];

console.log(one, two, three); // 1 2 3
```

```
const arr = [1, 2, 3];

const [one, two, three] =arr;

console.log(one, two, three); //1  2 3
```

```
const [x, y] = [1, 2];
```

```
const [x, y]; // SyntaxError
const [a, b] = {}; //TypeError
```

```
let x, y;
[x, y] = [1, 2];
```

```
const [a, b] = [1, 2];
console.log(a, b); // 1 2

const [c, d] = [1];
console.log(c, d); // 1 undefined

const [e, f] = [1, 2, 3];
console.log(e, f); //1 2

const [g, , h]= [1, 2, 3];
console.log(g, h); // 1 3
```

```
const [a, b ,c =3] =[1, 2];
console.log(a, b, c); // 1 2 3

const [e, f = 10, g = 3] = [1, 2];
console.log(e, f, g); // 1 2 3
```

```
function parseURL(url = '') {
	const parsedURL = url.match(/^(\w+):\/\/([^/]+)\/(.*)$/);
	console.log(parsedURL);
	/*
	 [
    'https://developer.mozilla.org/ko/docs/Web/JavaScript',
    'https',
    'developer.mozilla.org',
    'ko/docs/Web/JavaScript',
    index: 0,
    input: 'https://developer.mozilla.org/ko/docs/Web/JavaScript',
    groups: undefined
  ]
	*/

	if(!parsedURL) return {};

	const [, protocol, host, path] = parsedURL;

	return { protocol, host, path};
}

const aprsedURL = parseURL('https://developer.mozilla.org/ko/docs/Web/JavaScript');

console.log(parsedURL);
/*
{
  protocol: 'https',
  host: 'developer.mozilla.org',
  path: 'ko/docs/Web/JavaScript'
}
*/
```

```
const [x, ...y] = [1, 2, 3];
console.log(x, y); //1 [2, 3]
```

## 객체 디스트럭처링 할당

```
var user = { firstName: 'Ungmo', lastName: 'Lee'};

var firstName = user.firstName;
var lastName = user.lastName;

console.log(firstName, lastName); //Ungmo Lee
```

```
const user = { firstName: 'Ungmo', lastName: 'Lee'};

const {lastNAme, firstName} = user;

console.log(firstName, lastName); //Ungmo Lee
```

```
const { lastName, firstName} = {firstName: 'Ungmo', lastName: 'Lee'};
```

```
const { lastName, firstName}; //SyntaxError

const { lastName, firstName} = null;//TypeError
```

```
const { lastName, firstName} = user;

const { lastName: lastName, firstName: firstName} = user;
```

```
const user = { firstName: 'Ungmo', lastName: 'Lee'};

const { lastName: ln, firstName: fn} = user;

console.log(fn, ln); // Ungmo Lee
```

```
const { firstName = 'Ungmo', lastName} = {lastName: 'Lee'};
console.log(firstName, lastName); //Ungmo Lee

const {firstName: fn = 'Ungmo', lastName: ln} ={ lastName: 'Lee'};
console.log(fn, ln); //Ungmo Lee
```

```
const str = 'Hello';

const { length} = str;
console.log(length) ;// 5

const todo = { id: 1, content: 'HTML', compelted: true};

const { id } = todo;
console.log(id); // 1
```

```
function printTodo() {
	console.log(`할일 ${todo.content}은 ${todo.completed ? '완료' : '비완료'} 상태입니다.`);
}

printTodo( { id: 1, content: 'HTML', completed: true});
//할일 HTML은 완료 상태입니다.
```

```
function printTodo({content, completed}) {
	console.log(`할일 ${content}은 ${completed? '완료' : '비완료'} 상태입니다.`);
}

printTodo({ id: 1, content: 'HTML', completed: true});
```

```
const todos = [
	{ id: 1, content: 'HTML', completed: true},
	{ id: 2, content: 'CSS', completed: false},
	{ id: 3, content: 'JS', completed: false}
];

const [, {id}] = todos;
console.log(id); //2
```

```
const user = {
	name: 'Lee',
	address: {
		zipCode: '03068',
		city: 'Seoul'
	}
};

const { address: { city }} = user;
console.log(city); //Seoul
```

```
const { x, ...rest} = {x: 1, y: 2, z: 3};

console.log(x, rest); //1 {y: 2, z: 3}
```
