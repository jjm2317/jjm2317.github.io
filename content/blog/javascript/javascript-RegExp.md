---
title: javascript RegExp
date: 2020-12-14 13:24:46
category: "javascript"
draft: false
---

# javascript RegExp

## 정규표현식

**정의**

일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식언어

**기능**

- 문자열을 대상으로 패턴 매칭 기능 제공
  - 특정 패턴과 일치하는 문자열 검색 / 추출 / 치환

**예시**

휴대폰 전화번호

- num 3 - num 4 - num 4

```js
const tel = "010-1234-567팔";

const regExp = /^\d{3}-\d{4}-\d{4}$/;

regExp.test(tel); //false
```

## 정규 표현식 생성

- RegExp 생성자 함수
- 정규 표현식 리터럴

**표기**

```js
//시작, 종료기호 /
//패턴
//플래그

/regexp/i;
```

**리터럴**

- 패턴 , 플래그로 구성

```js
const target = "Is this all there is";

const regexp = /is/i;

regexp.test(target); // true
```

**RegExp 생성자 함수**

```js
new RegExp(pattern[, flags]);

const regexp = new RegExp(/is/i);//es6
// const regexp = new RegExp(/is/,'i');
// const regexp = new RegExp('is', 'i');

regexp.test(target);
```

## RegExp 메서드

**정규표현식 사용 메서드**

- RegExp.prototype.exec
- RegExp.prototype.test
- String.prototype.match
- String.prototype.replace
- String.prototype.search
- String.prototype.split

### RegExp.prototype.exec

- 매칭 결과를 배열로 반환
- 첫번째 검색결과만반환

```js
const target = "Is this all there is?";

const regExp = /is/;
console.log(regExp.exec(target));
//[ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
```

### RegExp.prototype.test

- 매칭결과를 불리언 값으로 반환

```js
const target = "Is this all there is";
const regExp = /is/;
regExp.test(target); //true
```

### String.prototype.match

- 매칭정보 배열로 반환
- g 플래그 지정시 모든 매칭결과 반환

```js
const target = "Is this all there is";
const regExp = /is/;
target.match(regExp);
//[ 'is', index: 5, input: 'Is this all there is?', groups: undefined ]
```

## 플래그

- 정규 표현식의 검색방식 설정
- 중요한 3개 플래그
  - i
    - 대소문자 구별 x
  - g
    - 패턴과 일치하는 모든 문자열 전역 검색
  - m
    - 행이 바뀌어도 패턴검색 계속

## 패턴

- 문자열의 일정한 규칙 표현

**형식**

- / 로 열고닫으며 따옴표 생략
  - 따옴표 포함시 패턴에 포함

**사용**

- 문자열 검색
- 임의의 문자열 검색
- 반복 검색
- OR 검색
- NOT 검색
- 시작 위치로 검색
- 마지막 위치로 검색

### 문자열 검색

- RegExp 메서드와 함께 이용

```js
const target = "Is this all there is";
let regExp = /is/;

regExp.test(target); // true

target.match(regExp); // 매칭 결과 반환

regExp = /is/i; // ignore case : 대소문자 구별하지 않고 검색
regExp = /is/gi; // ignore case : 대소문자 구별하지 않고 검색 / global : 대상 문자열내 전역 검색
```

### 임의의 문자열 검색

**.** 은 임의의 문자 한 개를 의미

```js
const target = "Is this all there is?";
let regExp = /.../g;

target.match(regExp);
```

### 반복 검색

**{m,n}**

- 앞선 패턴이 최소 m 번, 최대 n 번 반복되는 문자역
- , 뒤 공백있으면 정상동작 하지 않는다

```js
const target = "A AA B BB Aa Bb AAA";

const regExp = /A{1,2}/g;

target.match(regExp); //  ["A", "AA", "A", "AA", "A"]
```

**{n}**

- {n,n}과 동치

**{n,}**

- 앞선 패턴이 최소 n번 이상 반복

**+**

- {1,}와 동치

```js
const target = "A AA B BB Aa Bb AAA";

let regExp = /A{1,2}/g;

regExp = /A{1}/g;
regExp = /A{1,}/g;
regExp = /A+/g;

target.match(regExp);
```

**?**

- 앞선 패턴이 최대 한 번 이상 반복되는 문자열
- {0,1} 과 동치

```js
const target = "color colour";

const regExp = /colou?r/g;

console.log(target.match(regExp));
//[ 'color', 'colour' ]
```

### OR 검색

**|**

- or 의 의미를 가짐

```js
const target = "A AA B BB Aa Bb";

let regExp = /A|B/g;

console.log(target.match(regExp));
// [
//     'A', 'A', 'A',
//     'B', 'B', 'B',
//     'A', 'B'
// ]
regExp = /A+|B+/g;
console.log(target.match(regExp));
//[ 'A', 'AA', 'B', 'BB', 'A', 'B' ]
```

**[ ]**

- [] 내의 문자는 or로 동작한다.

```js
regExp = /A+|B+/g;
console.log(target.match(regExp));
//[ 'A', 'AA', 'B', 'BB', 'A', 'B' ]

regExp = /[AB]+/g;
console.log(target.match(regExp));
//[ 'A', 'AA', 'B', 'BB', 'A', 'B' ]
```

**-**

- 범위지정

```js
const target = "A AA B BB Aa Bb";
regExp = /[A-Z]+/g;

console.log(target.match(regExp)); //[ 'A', 'AA', 'B', 'BB', 'A', 'B' ]
```

**알파벳 대소문자 미구별**

```js
const target = "AA BB Aa Ba 12";

const regExp = /[A-Za-z]+/g;

target.match(regExp);
```

**숫자 검색**

```js
const target = "A AA B 01 23 3445";
regExp = /[0-4]+/g;

console.log(target.match(regExp)); //[ '01', '23', '344' ]
```

```js
const target = "A AA B 01 23 3445 123,456";
regExp = /[0-9,]+/g;

console.log(target.match(regExp)); //[ '01', '23', '3445', '123,456' ]
```

**\d**

- 숫자를 의미
- \D 는 숫자가 아닌 문자를 의미

```js
const target = "A AA B 01 23 3445 123,456";
regExp = /[\d,]+/g;

console.log(target.match(regExp)); //[ '01', '23', '3445', '123,456' ]

regExp = /[\D,]+/g;
console.log(target.match(regExp)); //[ 'A AA B ', ' ', ' ', ' ', ',' ]
```

**\w**

- 알파벳, 숫자, 언더스코어
- [A-Za-z0-9]와 동치
- \W 는 \w와 반대로 동작

```js
const target = "11st_1080p@@@11st_720p";

let regExp = /\w+/g;
console.log(target.match(regExp)); //[ '11st_1080p', '11st_720p' ]
```

### NOT 검색

- [...] 내의 ^은 not

```js
//[^0-9]는 숫자를 제외한 문자
//\D 와 동치

//[^A-Za-z0-9_]
//\W 와 동치
```

### 시작 위치로 검색

- [...] 밖의 ^은 문자열의 시작을 의미한다.
- [...] 내의 ^ 은 not

```js
const target = "https://asdf";
let regExp = /^https:/;

console.log(regExp.test(target)); //true
```

### 마지막 위치로 검색

**$**

- 문자열의 마지막

```js
const target = "www.naver.com";
let regExp = /com$/;
console.log(regExp.test(target)); //true
```

## 자주 사용하는 정규 표현식

### 특정단어로 시작하는 지 검사

**http or https**

```js
const url = "https://www.google.com";

const regExp = /^https?:\/\//;
console.log(regExp.test(url)); //true
```

### 특정 단어로 끝나는지 검사

```js
const file = "index.html";

const regExp = /html$/;

console.log(regExp.test(file));
```

### 숫자로만 이루어진 문자열인지 검사

```js
const number = "123131";

const regExp = /^\d+$/;
console.log(regExp.test(number));
```

### 하나이상의 공백으로시작하는지 검사

**\s**

- 공백 문자를 의미

```js
const target = " 123123";
const regExp = /^\s+/;

console.log(regExp.test(target));
```

### 아이디로 사용 가능한지 검사

```js
const id = "wlaks2317";

const regExp = /^[a-zA-Z0-9]{4,10}$/;

console.log(regExp.test(id));
```

### 메일 주소 형식에 맞는지 검사

```js
const email = "wlaks2317@gmail.com";

/^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/.test(
  email
);
```

### 핸드폰 번호 형식에 맞는지 검사

```js
const phoneNum = "010-9453-3317";

const regExp = /^\d{3}-\d{3,4}-\d{4}$/;

console.log(regExp.test(phoneNum)); //true
```

### 특수 문자 포함 여부 검사

```js
const target = "231!232$%";

let regExp = /[^A-Za-z0-9]/gi;

console.log(regExp.test(target));

console.log(/[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]/gi.test(target));

const newTarget = target.replace(regExp, "");
console.log(newTarget); //231232
```
