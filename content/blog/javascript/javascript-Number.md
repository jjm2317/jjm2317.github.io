---
title: javascript Number
date: 2020-10-22 15:43:43
category: "javascript"
draft: false
---

# Number

## 1. Number 생성자 함수

```
const numObj = new Number();
console.log(numObj); // Number {[[PrimitiveValue]]: 0}
```

```
const numObj = new Number(10);
console.log(numObj); //Number {[[PrimitiveValue]] : 10}
```

```
let numObj = new Number('10');
console.log(numObj); // Number {[[PrimitiveValue]]: 10}
numObj = new Number('Hello');
console.log(numObj); // Number {[[PrimitiveValue]]: NaN}
```

## 2. Number 프로퍼티

### 2.1 Number.EPSILON

```
0.1 + 0.2;//0.30000000000000004
0.1 + 0.2 === 0.3;// false
```

```
function isEqual(a,b){
	return Math.abs(a-b) < Number.EPSILON;
}

isEqual(0.1 + 0.2, 0.3); //true
```

### 2.2 Number.MAX_VALUE

```
Number.MAX_VALUE; // 1.7976931348623157e+308
Infinity > Number.MAX_VALUE
```

### 2.3 Number.MIN_VALUE

```
Number.MIN_VALUE; // 5e-324
NUMBER.MIN_VALUE > 0;//true
```

### 2.4 NUMBER.MAX_SAFE_INTEGER

```
Number.MAX_SAFE_INTEGER; // 9007199254740991
```

### 2.5 Number.MIN_SAFE_INTEGER

```
Number.MIN_SAFE_INTEGER; //-9007199254740991
```

### 2.6 Number.POSITIVE_INFINITY

```
Number.POSITIVE_INFINITY; //Infinity
```

### 2.7 Number.NEGATIVE_INFINITY

```
Number.NEGATIVE_INFINITY; // -Infinity
```

### 2.8 Number.NaN

```
Number.NaN; // NaN
```

## 3. Number 메서드

### 3.1 Number.isFinite

```
Number.isFinite(0);
Number.isFinite(Number.MAX_VALUE); //true
Number.isFinite(Number.MIN_VALUE)l //true

Number.isFinite(Infinity); //false
Number.isFinite(-Infinity); // false
```

```
Number.isFinite(NaN); // false
```

```
Number.isFinite(null) ;// false

isFinite(null); //true
```

### 3.2 Number.isInteger

```
Number.isInteger(0); // true
Number.isInteger(123); //true
Number.isInteger(-123); //true

Number.isInteger(0.5); //false
Number.isInteger('123'); //false
Number.isInteger(false); //false
Number.isInteger(Infinity); //false
Number.isInteger(-Infinity); //false
```

### 3.3 Number.isNaN

```
Number.isNaN(NaN); //true
```

```
Number.isNaN(undefined); //false
isNaN(undefined); //false
```
