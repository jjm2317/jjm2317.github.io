---
title: javascript 09Casting&ShortCircuit
date: 2020-08-26 21:45:20
category: "javascript"
draft: false
---

# 타입 변환과 단축 평가

## 타입 변환이란?

- 자바 스크립트의 모든 **값**에는 타입이 있다.
- 타입 변환은 값의 타입을 변환시키는 것이다.

타입 변환이 일어나는 방식은 두가지이다.

1. 개발자의 의도에 의한 타입 변환
2. 자바스크립트 엔진에 의해 자동으로 수행되는 타입변환

### 개발자가 의도적으로 타입변환 : 명시적 타입변환

- 개발자가 의도적으로 타입을 변환하는 것을 명시적 타입변환(explicit coercion) 또는 타입 캐스팅(type casting) 이라고 한다.

#### 예시

```
var num = 100;
//식별자 num 에 할당된 값의 타입은 number 이다
var str = num.toString();
console.log(num, str); // 10 10
console.log(typeof num, typeof str); // number string

// string 타입으로 타입 캐스팅하였다.
// num 의 메모리에 할당된 값을 변경한 것은 아니고 새로운 메모리 공간을 확보하여 string 10 을 저장 하였다.
```

### 개발자의 의도와 상관없이 타입변환 : 암묵적 타입변환

- 자바스크립트 엔진에 의해 타입이 자동변환된다.
- 특정 상황에서 **표현식을 평가**할 때 일어난다.
- 암묵적 타입 변환(implicit coercion) 또는 타입 강제 변환(type coercion) 이라고 한다.

#### 예시

```
var x = 100;

var str = x + '';
// + 연산자는 피연산자에 문자열이 있으면 연결 연산자로 동작한다.
// x에 할당된 값 100은 '100' 으로 강제 형변환

console.log(x,str); // 100 100
console.log(typeof x, typeof str); number string

//개발자의 의도와 상관없이 number 타입이었던 100이 string 타입으로 변경됨
// 암묵적 타입변환도 기존 number 타입의 값을 '변경'한 것이 아니며, string 타입의 값을 '생성' 한것이다.

//원시값(primitive value)은 변경 불가능한 점 기억하자
```

### 코드를 예측할 수 있는 것이 중요하다(feat.타입변환)

**명시적 타입변환**의 경우, 코드에 타입변환의 의도가 명백히 드러난다.

**암묵적 타입변환**의 경우, 타입변환의 의도가 명백히 드러나지는 않는다.

암묵적 타입변환에 대해 잘 이해하지 못한다면, 뜻밖의 오류가 발생할 수 있으며, 결과를 예측하기 어려워진다. 암묵적타입변환은 왜 쓰이는 것일까?

본래의 경우, **html css 사용자의 편의를 고려**한 자바스크립트의 **탄생배경**과 관련이 있다. **편의를 대가로 오류예측의 어려움**이 생겼지만, 암묵적 타입변환을 잘 이해하고 있다면 다음과 같은 장점이 있다.

- 명시적 타입변환에 비해 간결한 코드를 작성 가능
- 문법을 이해하고 있다는 가정 하에, 가독성이 더 좋은 코드 작성 가능

결론은, 타입변환의 원리를 이해하도록 하자

그렇다면, 이번챕터의 이슈인 암묵적 타입변환을 먼저 다루어보자.

## 1. 암묵적 타입변환

- 자바스크립트 엔진이 코드의 **문맥**을 고려해 데이터타입을 강제 변환

### '문맥'을 고려?

프로그램내에 여러 상황이 있다.

- 조건식을 평가하여 코드의 실행 여부를 결정
- 숫자 끼리의 산술 연산
- etc...

조건식을 평가해서 boolean 값을 도출해야되는데 뜬금없이 숫자 가나온다면?

숫자끼리 산술 연산을 수행하는데 문자열이 나온다면?

: **문맥**에 맞지 않는다

다른 strict 한 언어들은 에러메시지를 출력한다. 하지만,

_자바스크립트는 문맥까지 생각해주는 친절한 언어이다._

#### 예시

```
20*'3'; // 60
// 문자열 3이 등장했지만 자바스크립트엔진은 *가 산술연산자임을 고려해서 3을 number로 암묵적으로 변환해 반환하였다(number3을 새로 생성)

20 + '3'; //'203'
// + 는 산술연산자, 연결연산자 쓰인다. 엔진은 피연산자에 문자열이 있으면 +연산자의 경우 연결연산자로 동작하도록 설계된 듯 하다. '문맥'에 맞게 number 20을 string '20'으로 변환

if(3){};
// 조건식 부분에 number3 이 들어가 있다. 엔진은 number3 을  boolean true 로 강제 타입변환하여 값을 생성한다.

```

암묵적 타입변환의 여러 경우를 자세히 살펴보자

### 1.1 문자열 타입으로 변환

문맥상 값이 문자열 타입으로 변환되어야 되는 경우는 여러경우가 있다.

- +연결 연산자의 피연산자들
- 템플릿 리터럴의 표현식 삽입에서 작성된 표현식

문자열 타입변환은 대부분 + 연결연산자와 함께 일어난다.

#### 예시

```
//숫자 타입
//음수와 양수구분까지 처리한다. 즉 - 단항연산자까지 반영
0 + ''; // '0'
-0 + ''; // '0' 음수 0 은 음수고려안한다
1 + '' ; // "1"
-1 + ''; // '-1'
NaN + ''; // 'NaN'
Infinity + ''; // 'Infinity'
-Infinity + ''; // '-Infinity';

//boolean
true + ''; // 'true'
false + ''; // 'false'

//null
null + ''// 'nul'

undefined + ''; //"undefined"

//symbol
(Symbol())+ '' // TypeError 출력

//객체 타입
({}) + ''; // "[object Object]"
Math + ''; // "[object Math]"
[] + '';
[10, 20] + ''; // "10,20"
(function(){}) + ''; //"function(){}"
Array + ''; // "function Array(){[native code]}"
```

### 1.2 숫자 타입으로 변환

문맥상 값이 숫자 타입으로 변환되어야 하는 경우가 있다.

- +이외의 산술 연산자( - \* / %)의 피연산자
- +단항 연산자의 피연산자
- <> 비교 연산자의 피연산자

```
// 문자열 타입
+''       // -> 0
+'0'      // -> 0
+'1'      // -> 1
+'string' // -> NaN 변환해도 실수가 아닌경우 NaN 반환

// 불리언 타입
+true     // -> 1
+false    // -> 0

// null 타입
+null     // -> 0

// undefined 타입
+undefined // -> NaN

// 심벌 타입
+Symbol() // -> typeError: Cannot convert a Symbol value to a number

// 객체 타입
+{}             // -> NaN
+[]             // -> 0
+[10, 20]       // -> NaN
+(function(){}) // -> NaN
```

### 1.3 불리언 타입으로 변환

문맥상 값이 boolean 타입이 되어야 되는 경우는 다음과같다

- 반복문의 조건식
- 조건문의 조건식

즉 제어문의 조건식은 boolean 값으로 평가되어야 하기 때문에 자동 타입변환이 일어난다.

```
if('') console.log('1');
if(true) console.log('2');
if(0) console.log('3');
if('str') console.log('4');
if(null) console.log('5');

//2 4
```

타입 변환이 일어날때 **false로 평가되는 값은 한정적**이므로 false로 평가되는 값들을 알고 나머지는 true로 평가된다고 생각하면 좀 더 편리하다.

값이 boolean타입으로 평가될때 두가지로 평가된다.

- Truthy 값 : 참으로 평가되는 값 (평가값 true)
- Falsy 값 : 거짓으로 평가되는 값 (평가값 false)

#### Falsy 값(false로 평가되는 값)

- false
- undefined
- null
- 0, -0
- NaN
- ''

```
var values = [false, undefined, null, 0 , NaN, '','0',true, {}, []];//falsy인지 truthy인지 판별할 값들
var falsyList = [];
var truthyList

//Truthy/Falsy 를 판별하는 함수
function isFalsy(v){
	return !v;
}
function isTrue(v){
	return !!v;
}

//values 값들이 falsy인지 판별해보자

for(var i of values){
	if(isFalsy(i)){
		falsyList.push(i);
	}
}
console.log(falsyList);
//[ false, undefined, null, 0, NaN, '' ]

//values 값들이 truthy 인지 판별해보자
for (var j of values){
	if(isTruthy(j)){
		truthyList.push(j);
	}
}
console.log(truthyList);
//[ '0', true, {}, [] ]
// '0'이 true이다. 빈문자열이 아니면 true로 변환된다.




//별개로 의문점
//console.log(falsyList + '는 falsy 값');
//배열 안의 undefined,null 은 배열을 문자열 변환시 사라진다.왜일까
```

## 2. 명시적 타입 변환

- 개발자의 의도에 따라 명시적으로 타입을 변경할 수 있다.
- 보통 다음 3가지 방법을 따른다
  - 표준 빌트인 생성자 함수(String, Number, Boolean)를 new 없이 호출
  - 빌트인 메서드
  - 암묵적 타입변환 이용

표준 빌트인 생성자 함수와 빌트인 메서드는 자바스크립트에서 기본제공 함수이다.

### 2.1 문자열 타입으로 변환

위에서 제시한 세가지 방법으로 값을 문자열 타입으로 변환시켜보자

1. String 생성자 함수를 new 연산자 없이 호출

2. Object.prototype.toString 메서드

3. 문자열 연결 연산자

#### 1. String 생성자 함수를 new 연산자 없이 호출

```
//데이터 타입 : number boolean undefined null symbol, object >> string

//1. String 생성자 함수를 new 연산자 없이 호출

//1.1 number to string
String(1); // '1'
String(NaN);// 'NaN'
String(-0); // '0'
String(-Infinity); // '-Infinity'

//1.2 boolean to string
String(true); // 'true'
String(false); // 'false'

//1.3 undefined to string
String(undefined); // 'undefined'

//1.4 null to string
String(null); // 'null'

//1.5 symbol to string
String(Symbol()); // 'Symbol()' 연결연산자로는 안되던게 1 방식에서는 된다!

//1.6 object to string
String({}); // '[object Object]'
String([]); // ''
String([1,2]); // '1,2'
String(Array); // 'function Array() { [native code] }'
String(Math); // '[object Math]'

```

#### 2. Object.prototype.toString 메서드 이용

```
//데이터 타입 : number boolean undefined null symbol, object >> string

//2. Object.prototype.toString 메서드 이용

//2.1 number to string
(1).toString(); // '1'
(NaN).toString();// 'NaN'
(-0).toString(); // '0'
(-Infinity).toString(); // '-Infinity'

//2.2 boolean to string
(true).toString(); // 'true'
(false).toString(); // 'false'

//2.3 undefined to string
(undefined).toString(); // typeError 뜨는데.. 왜그럴까

//2.4 null to string
(null).toString(); // 이것도 typeError

//2.5 symbol to string
(Symbol()).toString(); // 'Symbol()' 빌트인 메서드도 된다

//2.6 object to string
({}).toString(); // '[object Object]'
([]).toString(); // ''
([1,2]).toString(); // '1,2'
(Array).toString(); // 'function Array() { [native code] }'
(Math).toString(); // '[object Math]'


// undefined,null 타입을 제외하곤 String 생성자함수와 동일한결과
```

#### 3. 문자열 연결 연산자

- 암묵적 타입변환에서 다루었으므로 생략

### 2.2 숫자 타입으로 변환

역시나 크게 세가지 방법이 있다.

1. Number 생성자 함수 new 연산자 없이 호출
2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
3. 산술 연산자 이용
   - +단항 산술 연산자
   - \*산술 연산자

#### 1. Number 생성자 함수 new 연산자 없이 호출

```
//데이터 타입 : string boolean undefined null symbol, object >> number

//1. Number 생성자 함수 new 연산자 없이 호출

//1.1 string to number
Number('0'); // 0
Number('5.12'); // 5.12
Number(''); // 0 빈 문자열 은 0으로 변환


//1.2 boolean to number
Number(true); // 1
Number(false); // 0

//1.3 undefined to number
Number(undefined); // NaN

//1.4 null to number
Number(null); //  0

//undefined 는 NaN, null은 0으로 변환된다.

//1.5 symbol to number
Number(Symbol()); // TypeError 발생한다. String 생성자 함수로 가능했지만 Number에서는 안된다.

//1.6 object to number
Number({}); // NaN
Number([]); // 0
Number([1,2]); // NaN
Number(Array); // NaN
Number(Math); // NaN
// 빈 배열을 제외하고는 NaN으로 변환된다.



```

#### 2. parseInt, parseFloat 함수를 사용하는 방법

```
// 문자열만 변환 가능하다

parseInt('0'); // 0
parseInt('3.22')// 3 소수점을 무시하고 정수반환
parseFloat('3.22')// 3.22

```

#### 3. 산술 연산자 이용(+, \* 를 이용한 암묵적 타입변환)

```
//데이터 타입 : string boolean undefined null symbol, object >> number

//3. 산술 연산자 이용(+, * 를 이용한 암묵적 타입변환)

//3.1 string to number
+'0';
1 * '0'
// 0

+'5.12';
1 * '5.12'';
// 5.12

+'';
1 * '';
// 0 빈 문자열 은 0으로 변환

2 * '5';//10


//3.2 boolean to number
+true;
1 * true;
// 1
2 * true; // 2

+false;
1 * false;
// 0

//3.3 undefined to number
+undefined;
1 * undefined;
// NaN

//3.4 null to number
+null;
1 * null;
//0


//3.5 symbol to number
+Symbol();
1 * Symbol();
// TypeError 발생한다.

//3.6 object to number
// 마찬가지로, 빈배열이 0으로 변환되는 것을 제외하고 전부 NaN
```

#### 3. boolean 타입으로 변환

boolean 타입으로 변환하는 방법은 두가지!

1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
2. ! 부정 논리 연산자를 두번 사용하는 방법

명시적 타입변환에서도 다음만 고려하면 된다!

##### Falsy 값(false로 평가되는 값)

- false
- undefined
- null
- 0, -0
- NaN
- ''

```
//1 string to boolean (only '')
Boolean('x');       // true
Boolean('');        // false
Boolean('false');   // true
!! 'x' ; // true
!! ''; // false
!! 'false'//true

//2 undefined
Boolean(undefined); // false
!!(undefined); // false

//3 null
Boolean(null); //  false
!! null; // false

//4 0, -0
Boolean(0);//false
!!0 ; // false

//5 NaN
Boolean(NaN);// false
!!NaN;//false
```

## 3. 단축 평가

논리 연산의 결과를 결정하는 피연산자를 **타입 변환 없이** 그대로 반환하는 것

if 문을 대체할 수 있다.

### 3.1 논리 연산자를 사용한 단축 평가

#### issue

- **논리합 연산자와 논리곱 연산자**의 평가 결과가 불리언 값이 **아닐 수도** 있다.
- 표현식 **평가 도중에 평가 결과가 확정**되면 **나머지 평가 과정을 생략**

: 표현식의 평가과정이 생략될 수도 있다!!

논리곱 / 논리합 연산자 사용 예시를 통해 단축평가의 개념을 알아보자

#### 논리곱/논리합 연산자의 평가 결과가 불리언 값이 아닐 수 있다.

```
'Html' && 'CSS'; // 'CSS'
'Html' || 'CSS'; // 'Html'
//boolean 값이 아닌 문자열 피연산자가 그대로 반환된다.
```

여기서 알아야 될 **논리합/논리곱 연산자 표현식의 평가 과정**!

- 좌항에서 우항으로 평가가 진행된다.
- 평가 진행 도중 평가 결과가 확정될 수 있다

그리고 **중요!**한 특징

- 평가 결과가 확정되면 타입 변환 없이 그대로 반환한다.
  - 즉 일반적으로 타입변환까지 해서 평가과정을 마무리하는 다른 연산자 표현식과는 차이가 있다.

위 코드 예시에서 && 연산자 표현식을 먼저 보자

##### 두번째 피연산자가 평가결과를 결정

'Html' 이 Truthy 값이므로 true이다. 하지만 **&&연산자 특성상** 이 시점에서 평가가 끝나지 않는다. 우항의 피연산자도 평가를 해야지 연산자 표현식의 평가 결과를 결정할 수 있다. 즉 **평가 결과는 두번째 피연산자인 'CSS'** 가 결정한다.

##### 평가결과가 확정된 시점에 평가 과정을 종료

첫번째가 true로 평가되서 **두번째 피연산자인 'CSS'로 평가 결과가 확정**되었다. 논리 연산의 특성상 boolean 값으로 타입변환해서 true를 반환해야될것 같지만 'CSS' 로 **평가 결과가 확정된 시점에 평가 과정을 종료**하는 **단축평가**가 이루어져, **'CSS' 를 타입변환없이 그대로 반환**한다.

**논리합 연산자**는 어떨까??

##### 첫번째 피연산자가 평가 결과를 결정

|| 연산자 특성상 평가 결과중 true가 하나라도 있으면 평가 결과가 확정된다. 즉 Truthy 값인 'Html' 이 평가 결과를 결정한다. 두번째 피연산자는 평가를 시행하지않는다.

##### 평가 결과가 확정된 시점에 평가 과정을 종료

'Html'로 평가 결과가 확정되었기 때문에 두번째 피연산자의 평가는 시행하지 않는다. 마찬가지로, 타입변환도 실행하지 않고 평가를 종료한다. 'Html' 이 타입변환없이 그대로 반환

그럼, 두가지 연산자의 단축평가에 따른 결과를 정리해보자

| 단축 평가 표현식    | 평가 결과 |
| ------------------- | --------- |
| true \|\| anything  | true      |
| false \|\| anything | anything  |
| true && anything    | anything  |
| false && anything   | false     |

#### 단축평가는 어디에 이용될까?

제어문을 사용한다면 코드의 흐름을 제어하게 된다. 제어문은 가독성을 떨어뜨리는 요소이기 때문에 단축평가를 사용하여 대체할 수 있다.

일반적으로

1. if 문 대체
2. 객체를 할당한 변수의 타입을 재확인할 때
   - 변수가 falsy 값인상태에서 프로퍼티를 참조하면 에러 및 프로그램 종료된다.
3. 함수 매개변수에 기본값 설정

##### if 문 대체

```
var correct, sign;
correct = true;

if(correct){
	sign = 'complete';
}

// sign = correct && 'complete';

if(!correct){
	sign = 'fail';
}

// sign = correct || 'fail';

//여기까지는 그렇게 유용한가 싶다.
```

##### 객체를 할당한 변수의 타입을 재확인할때 (돌다리 두드려볼때)

객체의 프로퍼티를 참조하려는 상황이다.

```
var elem = null;
//elem 변수에는 객체가 할당되어있다고 예상했지만, null 인 상황을 가정
var value = elem && elem.value;// null

// null 인 변수의 프로퍼티를 참조하려고하면 에러가 나기때문에 위와같이 에러 및 프로그램 종료를 방지할 수 있다.
```

##### 함수 매개변수에 기본값을 설정할 때

- 먼저 설명하자면, 매개변수가 있는 함수를 호출할 때 인수를 작성하지 않으면 undefined가 할당된다. 이로 인한 오류들을 방지하기 위해 사용

```
function getStringLength(str){
	str = str || '';
	return str.length;
}
//문자열 길이를 측정하는 함수이다(웅모강사님 코드)

getStringLength(); //0
//undefined에서 length 프로퍼티를 참조하면 발생하는 에러를 방지한다.

//es6 에서는 다음과 같이 매개변수 기본값을 설정한다
function getStringLength(str = ''){
	return str.length;
}

```

### 3.2 옵셔널 체이닝 연산자

3.1 에서 단축평가를 통해 **객체를 할당한 변수의 타입을 재확인**하는 과정이 있었다.

```
var elem = null;

var value = elem && elem.value;// null
```

옵셔널 체이닝 연산자 ?. 도 이와 같은 방식이다.

```
var elem = null;

var value = elem?.value;// null

//elem이 Truthy 값이면 value 참조를 이어간다.
// &&연산자와의 차이가 있다면 &&연산자 표현식은 단축평가의 특성을 이용했다면, ?.연산자 표현식은 프로퍼티 참조에 포커스를 둔 것?이다
```

#### 기존 단축평가를 통한 프로퍼티참조의 문제점 개선

&&연산자 표현식을 통한 객체 평가에서, 좌항이 0이나 ''이면 false로 평가되었다. 하지만 0, ''를 객체로 평가하는 경우도 있다. ?.연산자 표현식에서는 프로퍼티 참조에 있어서 이러한 문제를 개선하였다.

```
var str = '';
var length = str && str.length;
console.log(length);//''
//0 을 기대하였지만 ''는 falsy 값이므로 ''그대로 반환된다.

//옵셔널 체이닝 연산자 ?.를 통해 이를 개선해보자
var length = str ?.length;
console.log(length);//0
```

### 3.3 null 병합 연산자

3.1 에서 논리합연산자 (||) 를통한 단축평가와 비슷하지만 조금 다르게, 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고 아닌 경우 좌항을 반환한다.

#### || 연산자를 통한 단축평가와는 어떤 차이가 있을까

- falsy 값 전부를 false 로 평가하여 우항을 반환하는 || 연산자 표현식과 다르게,
- null 과 undefined인 경우에만 우항을 반환

##### '' 이나 0을 유효한 값으로 판단

```
var foo = '' ?? 'falsy';
console.log(foo); // ''
```
