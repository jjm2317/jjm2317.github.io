---
title: javascript control-flow-exercise
date: 2020-09-07 18:38:56
category: "javascript"
draft: false
---

# Exercise (삼항 조건 연산자 , 제어문)

## 과제 1

아래 코드를 삼항 조건 연산자로 변경

```
var x = 11;
var res;
if (x === 0) {
  res = '영';
} else if (x % 2 === 0) {
  res = '짝수';
} else {
  res = '홀수';
}
```

**Answer**

```
var x = 11;
var res = x % 2 === 0 ? (x === 0  ? '영' : '짝수') : '홀수';
```

## 과제 2

제어문 연습문제 풀이

### 1. 변수 x가 10보다 크고 20보다 작을 때 변수 x를 출력하는 조건식을 완성하라

```
var x = 15;

// 변수 x가 10보다 크고 20보다 작을 때 변수 x를 출력하는 조건식을 완성하라.
if (...) {
  console.log(x);
}
```

**Answer**

```
var x = 15;

if (x > 10 && x < 20) {
  console.log(x);
}
```

### 2. for문을 사용하여 0부터 10미만의 정수 중에서 짝수만을 작은 수부터 출력하시오.

```
0
2
4
6
8
```

**Answer**

```
for(var number = 0; number < 10; number++){
	if(number % 2 === 0){
		console.log(number);
	}
}
```

### 3. for문을 사용하여 0부터 10미만의 정수 중에서 짝수만을 작은 수부터 문자열로 출력하시오.

```
02468
```

**Answer**

```
var result='';

for(num = 0; num < 10; num++){
	if(num % 2 === 0){
		result += num;
	}
}

console.log(result);
```

### 4. for문을 사용하여 0부터 10미만의 정수 중에서 홀수만을 큰수부터 출력하시오.

```
9
7
5
3
1
```

**Answer**

```
for(var num = 9; num >= 0; num--){
	if(num % 2 === 1){
		console.log(num);
	}
}
```

### 5. while문을 사용하여 0 부터 10 미만의 정수 중에서 짝수만을 작은 수부터 출력하시오.

```
0
2
4
6
8
```

**Answer**

```
var num = 0;
while(num<10){
	if(num % 2 ===0){
		console.log(num)
	}
	num ++;
}
```

### 6. while문을 사용하여 0 부터 10 미만의 정수 중에서 홀수만을 큰수부터 출력하시오.

```
9
7
5
3
1
```

**Answer**

```
var num = 9;
while(num >= 0){
	if(num % 2 ===1){
		console.log(num)
	}
	num --;
}
```

### 7. for 문을 사용하여 0부터 10미만의 정수의 합을 출력하시오.

```
45
```

**Answer**

```
var sum = 0;

for(num = 0; num < 10; num ++){
	sum += num;
}
console.log(sum);
```

### 8. 1부터 20 미만의 정수 중에서 2 또는 3의 배수가 아닌 수의 총합을 구하시오.

```
73
```

**Answer**

```
var sum = 0;

for(num = 1; num < 20; num ++){
	sum += (num % 2 === 0 || num % 3 === 0) ? 0 : num;
}
console.log(sum);
```

### 9. 1부터 20 미만의 정수 중에서 2 또는 3의 배수인 수의 총합을 구하시오.

```
117
```

**Answer**

```
var sum = 0;

for(num = 1; num < 20; num ++){
	sum += (num % 2 === 0 || num % 3 === 0) ? num : 0;
}
console.log(sum);
```

### 10. 두 개의 주사위를 던졌을 때, 눈의 합이 6이 되는 모든 경우의 수를 출력하시오.

```
[ 1, 5 ]
[ 2, 4 ]
[ 3, 3 ]
[ 4, 2 ]
[ 5, 1 ]
```

**Answer**

```
for(var num1 = 1; num1 <= 6; num1 ++){
	for(var num2 = 1; num2 <= 6; num2 ++){
		if(num1 + num2 === 6){
			console.log(`[ ${num1}, ${num2} ]`);
		}
	}
}

```

### 11. 삼각형 출력하기 - pattern 1

다음을 참고하여 \*(별)로 높이가 5인(var line = 5) 삼각형을 문자열로 완성하라. 개행문자(‘\n’)를 사용하여 개행한다. 완성된 문자열의 마지막은 개행문자(‘\n’)로 끝나도 관계없다.

```
// 높이(line)가 5
*
**
***
****
*****
```

**Answer**

```
var line = 5;
var star = '';
var tri = '';
for(var i = 0; i < line; i++){
	star += '*';
	tri += star + '\n';
}
console.log(tri);
```

### 12. 삼각형 출력하기 - pattern 2

다음을 참고하여 \*(별)로 트리를 문자열로 완성하라. 개행문자(‘\n’)를 사용하여 개행한다. 완성된 문자열의 마지막은 개행문자(‘\n’)로 끝나도 관계없다.

```
*****
 ****
  ***
   **
    *
```

**Answer**

```
var line = 5;
var tri = '';
for(var i = 0; i < line; i++){
	for(var j = 0; j < i; j ++){
		tri += ' ';
	}
	for(var k = 0; k < line - i; k ++){
		tri += '*';
	}
	tri += '\n';
}
console.log(tri);
```

### 13. 삼각형 출력하기 - pattern 3

다음을 참고하여 \*(별)로 트리를 문자열로 완성하라. 개행문자(‘\n’)를 사용하여 개행한다. 완성된 문자열의 마지막은 개행문자(‘\n’)로 끝나도 관계없다.

```
*****
****
***
**
*
```

**Answer**

```
var line = 5;
var tri = '';
for(var i = 0; i < line; i++){
	for(var k = 0; k < line - i; k ++){
		tri += '*';
	}
	for(var j = 0; j < i; j ++){
		tri += ' ';
	}
	tri += '\n';
}
console.log(tri);
```

### 14. 삼각형 출력하기 - pattern 4

다음을 참고하여 \*(별)로 트리를 문자열로 완성하라. 개행문자(‘\n’)를 사용하여 개행한다. 완성된 문자열의 마지막은 개행문자(‘\n’)로 끝나도 관계없다.

```
    *
   **
  ***
 ****
*****
```

**Answer**

```
var line = 5;
var tri = '';
for(var i = 1; i <= line; i++){
	for(var j = 0; j < line - i; j ++){
		tri += ' ';
	}
	for(var k = 0; k < i; k ++){
		tri += '*';
	}
	tri += '\n';
}
console.log(tri);
```

### 15. 정삼각형 출력하기

```
    *
   ***
  *****
 *******
*********
```

**Answer**

```
var line = 5;
var tri = '';
for(var i = 1; i <= line; i++){
	for(var j = 0; j < line - i; j ++){
		tri += ' ';
	}
	for(var k = 0; k < i * 2 - 1; k ++){
		tri += '*';
	}
	tri += '\n';
}
console.log(tri);
```

### 16. 역정삼각형 출력하기

```
*********
 *******
  *****
   ***
    *
```

**Answer**

```
var line = 5;
var tri = '';
for(var i = 1; i <= line; i++){
	for(var j = 0; j < i - 1; j ++){
		tri += ' ';
	}
	for(var k = 0; k < (line - i) * 2 + 1; k ++){
		tri += '*';
	}
	tri += '\n';
}
console.log(tri);
```
