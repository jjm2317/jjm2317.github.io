---
title: javascript 10ObjectLiteral
date: 2020-08-27 22:10:26
category: "javascript"
draft: false
---

# 객체 리터럴

- 앞의 데이터 타입(data type) 에서 자바스크립트의 데이터 타입에는 원시 타입(primitive type)과 객체 타입(object/referrence type) 이 있다는 것을 알았다
- 리터럴은 값을 생성하는 표현식이다.
- 이번 챕터에서는 객체 리터럴(object literal), 즉 객체 값을 생성하는 표현식과 특징들을 알아볼 것이다.

## 1. 객체란?

자바스크립트가 **객체기반의 프로그래밍 언어**라는 말은 많이 들었다. 그렇다면 여기서 말하는 객체란 무엇일까?

자바스크립트 언어에는 여러 값(value)들이 있다.

- **원시 값(primitive value)를 제외한 모든 값**은 객체이다.
- 함수, 배열, 정규표현식 등은 모두 객체이다.

그렇다면 이 객체라는 값은 어떤 특징을 가지고 있을까??

원시값과 비교해보면,

- 원시 값은 **변경 불가한 값(immutable value)** 인 반면에, 객체는 **변경 가능한 값(mutable value)**이다.
- 원시 타입은 **하나의 값**만을 가지지만 객체 타입은 **여러 타입의 값**들을 하나의 묶음으로서 가진다.
  - 표현식이 원시타입으로 평가될 때 하나의 메모리에 저장된 하나의 값으로 평가된다.

객체의 특징을 객체의 구조와 함께 알아보자

### 1.1 객체의 구조

객체는 여러타입의 값들을 하나의 묶음으로 가진다고 하였다.

여기서 값들은 정확히는 0개 이상의 **프로퍼티** 를 나타낸다

#### 객체는 프로퍼티의 집합이다

**프로퍼티는 식별자의 상태(state), 동작을 나타낸다.**

- 객체는 프로퍼티(property)의 집합이다
- 프로퍼티는 키(key)와 값(value)로 구성된다.

```
var student = {
	name: 'Jiman', //프로퍼티
	age: 23 // 프로퍼티
};
//name, age 는 프로퍼티 키(key), 'Jiman', 23 은 각각 키에 대한 프로퍼티 값(value)이다/
```

- 프로퍼티 값은 **어떤 데이터 타입**도 가질 수 있다(원시값 or 객체)
  - 프로퍼티 값이 함수일 때 그 프로퍼티는 **메서드**라고 명명한다.

```
var gun = {
	bullet: 10, // 프로퍼티
	shot: function(){
		this.bullet--;
	} // 프로퍼티이다. 프로퍼티 값으로 객체 타입인 함수를 사용하였다.
};
// 프로퍼티 값이 함수일 경우 그 프로퍼티는 '메서드' 라고 한다.
```

메서드도 프로퍼티이지만 값으로 사용되는 프로퍼티와 구조와 사용방식이 다르므로 구분해서 설명해보자.

여기까지, 객체는 **프로퍼티와 메서드의 집합**이라는 것을 알 수 있다.

##### 프로퍼티와 메서드

- 프로퍼티 : 객체의 상태를 나타내는 **값(data)**
- 메서드 : 객체의 프로퍼티(data)를 참조하고 조작할 수 있는 **동작(behavior)**

#### 정리해보면!

- 객체는 자바스크립트의 값(value)이다. 원시값 이외는 모두 객체!

- 프로퍼티의 집합이다. 프로퍼티는 여러 타입의 값을 가질 수 있다.
- 프로퍼티 값이 객체일 수도 있으며 함수일 경우 그 프로퍼티를 메서드라고한다.

객체 지향 프로그래밍이란 **객체들의 집합**으로 프로그램을 표현하려는 프로그래밍 패러다임이다.

## 2. 객체 리터럴에 의한 객체 생성

지금까지 객체가 무엇인지 알아보았다. 이젠 객체라는 값을 생성할 수 있는 방법을 알아보자.

값을 생성하려고 할때 **표현식**을 작성하며, 특정 타입의 값을 표기 자체로 생성하려고 할때 표현식으로써 **리터럴**을 사용한다.

리터럴은 값을 나타내는 약속된 기호이다. **객체 값을 생성하는 리터럴**이 존재한다.

### 객체 리터럴의 사용

- 객체리터럴은 중괄호{} 안에 프로퍼티들을 정의하는 방식이다.

```
var cafe = {
	coffee: ['americano','latte', 'chocolate'],
	sales: [0,0,0],
	showMenu: function(){
		console.log(this.coffee.toString());
	},
	chooseCoffee: function(num){
		switch(num){
			case 1:
				this.sales[0]++;
				console.log('아메리카노 팔림');
				break;
			case 2:
				this.sales[1]++;
				console.log('라떼 팔림');
				break;
			case 3:
				this.sales[2]++;
				console.log('초콜릿 팔림');
				break;
		}
	}

};

console.log(typeof cafe); // object
console.log(cafe);
//{
  coffee: [ 'americano', 'latte', 'chocolate' ],
  sales: [ 0, 1, 0 ],
  showMenu: [Function: showMenu],
  chooseCoffee: [Function: chooseCoffee]
}

//지금 카페라서 한번 만들어봤다.
```

- 프로퍼티를 정의하지 않으면 빈 객체가 생성된다.

```
var cafe = {};
console.log(typeof cafe); // object
```

### 객체 리터럴은 코드블록과 다르다

코드 블록은 {} 안에 문들을 작성하는 방식으로 쓰인다는 점에서 객체 리터럴과 비슷하게 보인다. 하지만, 차이가 있다.

#### 객체 리터럴은 값으로 평가되는 표현식이다.

코드블록은 {} 안에 문들을 작성하는 블록문이다. 자체종결성이 있어 세미콜론을 붙이지 않는다.

그에반해, 객체리터럴은 표현식이다. 중괄호 뒤에 세미콜론을 붙인다.

여기까지, 객체의 개념과 객체를 생성하는 방법도 알았다. 지금부터는 객체에 대해 구체적으로 알아보자.

## 3. 프로퍼티

객체는 프로퍼티들의 집합이다. 이 프로퍼티들은 **키와 값**으로 구성된다.

- 프로퍼티는 세미콜론이 아닌, 쉼표로 구분한다.
- 마지막 프로퍼티 뒤에는 일반적으로 쉼표를 사용하지 않는다.

```
var myMajor = {
	name: 'Industrial Engineering',
	grade: 4.2
};
```

프로퍼티의 키(key), 값(value) 에는 어떤 값이 와야될까?

- 프로퍼티 키 : 빈 문자열' '을 포함하는 모든 **문자열** 또는 **심벌 값**
- 프로퍼티 값 : 자바스크립트의 모든 값

### 프로퍼티 키의 네이밍 규칙

프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름이다. 즉 **식별자** 역할을 한다.

식별자들은 일반적으로 식별자 네이밍 규칙을 따른다. 하지만 프로퍼티 키는 식별자 역할을 하지만 네이밍 규칙을 반드시 따라야 되는 것은 아니다. 즉, 식별자 네이밍 규칙을 준수할 수 도, 그렇지 않을수도 있다.

#### 프로퍼티 키는 어떻게 네이밍하는가

심벌 값 OR 문자열을 사용(**일반적으로 문자열을 사용한다**)

- 문자열은 따옴표로 묶어야하지만 식별자 네이밍 규칙을 준수하는 경우, 따옴표를 생략할 수 있다.
- 식별자 네이밍 규칙을 따르지 않는다면 따옴표를 사용해야한다.

`자바스크립트에서 식별자이름으로 쓸 수 있는 모든 표기는 식별자 네이밍 규칙을 준수한 것이다.`

```
var phoneNumber = {
	firstPin : 010,// 식별자 네이밍 규칙 준수
	'second-pin' : 9453, // 식별자 네이밍 규칙 미준수
}
```

식별자 네이밍 규칙을 준수한 프로퍼티키 firstPin은 따옴표를 사용하지 않았어도 문자열로 평가된다.

하지만 식별자 네이밍 규칙을 준수하지 않은 프로퍼티키 second-pin은 따옴표를 생략할 수 없다. 만약 따옴표를 생략한다면 자바스크립트 엔진은 - 연산자 표현식으로서 second-pin을 해석할 것이다.

##### 따옴표를 생략한다면?

```
var phoneNumber = {
	firstPin : 010,
	second-pin : 9453, // SyntaxError 발생
}
```

### 프로퍼티 키의 추가적인 특징

- 문자열 or 문자열로 평가되는 표현식으로, 프로퍼티 키를 동적을 생성가능하다.
  - 표현식을 대괄호 []로 묶어서 시용
- 빈문자열을 프로퍼티 키로 사용해도 에러가 발생하지 않음
  - but 의미가 없으므로 권장 안함
- 문자열, 심벌 값 이외의 값을 사용하면 문자열로 암묵적 타입변환된다.
- 예약어 (var, function 등) 를 프로퍼티 키로 사용가능하다
  - 권장하지는 않는다
- 기존에 있던 프로퍼티 키를 중복선언 하게되면 나중에 선언된 프로퍼티키가 먼저 선언한 프로퍼티 키를 덮어 쓴다.

```
//프로퍼티 키의 동적 생성
var student = {};
var key = 'name';

student[key] = 'jiman';
student['age'] = 23;

console.log(student); // { name: 'jiman', age: 23 }


// 빈 문자열을 프로퍼티 키로 사용해도 에러가 발생하지 않는다.
var emptyKey = {
	'': '';
}
console.log(emptyKey);
// {'': ''}


// 프로퍼티 키에 문자열 이외의 값(숫자 등)을 사용해도 암묵적 타입변환
var otherKey = {
	0: 'a',
	1: 'b',
	2: 'c'
};
console.log(otherKey);
// {0: 'a', 1: 'b', 2: 'c'}


//프로퍼티 키로 예약어 사용해도 에러발생 no
var usingReservedWord = {
	var: 'var',
	function: 'function'
};
console.log(usingReservedWord);
//{var: 'var', function: 'function'}


//프로퍼티 키 중복선언시 덮어씀
var overlapKey  = {
	age: 23,
	age: 24
};

console.log(overlapKey);
//{age: 24}
```

## 4. 메서드

객체의 프로퍼티 값(vale) 에는 자바스크립트의 모든 datatype의 값이 올 수 있다고 하였다.

datatype

- 원시값
- 객체

즉 원시값과 객체 값이 모두 올 수 가 있다. 함수는 **객체 타입의 값** 이다. 그렇다면 함수도 프로퍼티 값에 올 수 있다.

### 메서드: 함수를 프로퍼티 값으로 가지는 프로퍼티

함수가 객체의 프로퍼티 값으로 왔을때, 일반함수와의 구분을 위해서 메서드(method)라고 부른다. 즉 메서드는 객체안에 있는 함수이다.

일반적으로 메서드는 객체안의 프로퍼티를 참조하고, 조작할때 사용된다.

```
var musicPlayer = {
	songList: ['song1','song2','song3'],
	showList: function(){
		console.log(this.songList);
	}
};

console.log(musicPlayer.songList());
// [ 'song1', 'song2', 'song3' ]

```

## 5. 프로퍼티 접근

객체를 생성했다면. 해당 객체가 가지고 있는 프로퍼티를 이용하거나, 프로퍼티 값을 변경하기 위해 프로퍼티에 접근할 필요가 있다.

`객체의 프로퍼티에 어떻게 접근할 수 있을까 ?`

프로퍼티에 접근하기위해 연산자를 사용하는데, 두가지 방법이 있다.

- 마침표 표기법(dot notation) : 마침표 프로퍼티 접근연산자 . 사용
- 대괄호 표기법(bracket notation) : 대괄호 프로퍼티 접근 연산자[] 사용

프로퍼티 접근연산자는 객체로 평가되는 표현식 우측에 표기한다. 프로퍼티 접근연산자 마침표 . 우측에 / 프로퍼티 접근연산자 대괄호 [] 안에 프로퍼티 키를 표기한다.

대괄호 표기법의 경우 안의 키 이름을 따옴표로 감싸주어야한다. 대괄호 안의 키를 따옴표로 감싸지 않는다면 자바스크립트 엔진이 식별자로 해석한다.

```
var approach = {
	key = 'value'
} ;
// 마침표 표기법
console.log(approach.value); // value
// 대괄호 표기법
console.log(approach['key']);// value 키는 따옴표로 감싼다
// 대괄호 표기법에서 따옴표로 감싸지 않는다면
console.log(approach[key]); // ReferenceError 발생
```

`객체에 존재하지 않는 프로퍼티에 접근한다면?`

undefined 를 반환한다 (ReferenceError을 발생시키지 않는다.)

```
var obj = {
	key1 = ''
}

console.log(obj.key2); //undefined
```

`식별자 네이밍 규칙을 미준수한 프로퍼티에 접근하려면?`

다음과 같은 사항을 유의하자

- 반드시 대괄호 표기법 이용
- 프로퍼티 키가 숫자인 경우 따옴표 생략 가능
  - 그 외의 경우 따옴표로 감싼 문자열로 표기

```
//식별자 네이밍 규칙을 미준수한 프로퍼티 (ex -연산자 사용)
var person = {
	'last-name': 'Jeong',
	23: 'age'
};

//마침표 표기법으로 접근(에러)
person.'last-name';//SyntaxError
person.last-name; // 브라우저에서 NaN / Node.js 에서 ReferenceError

//대괄호 표기법으로 접근(따옴표 써줘야됨)
person[last-name]; //ReferenceError
person['last-name']; //Jeong

//단 프로퍼티가 숫자라면 따옴표 생략가능
person[23]; // age
person['23']; // age
```

## 6. 프로퍼티 값 갱신

이미 존재하는 프로퍼티의 값을 변경할 수 있다. 키를 직접 호출해(키에 접근해) 변경하거나 메서드를 이용할 수 있다.

```
var myAge = {
	age: 23
};

myAge.age=24;
console.log(myAge); // {age: 24}
```

## 7. 프로퍼티 동적 생성

객체 내에 존재하지 않는 프로퍼티를 임의로 표기하고 값을 할당하면 어떻게 될까?

프로퍼티가 동적으로 생성되며, 객체 내에 추가되고 프로퍼티 값도 할당된다.

```
var closet ={
	outer : 2
};

closet.inner = 5;
console.log(closet); // { outer: 2, inner: 5 }
```

## 8. 프로퍼티 삭제

객체 내의 프로퍼티를 삭제하고 싶다면 delete 연산자를 사용한다.

delete 연산자의 피연산자는 객체의 프로퍼티에 접근할 수 있는 표현식이어야한다. 주의할 점은 객체 내에 존재하지 않는 프로퍼티를 삭제해도 에러발생없이 넘어간다는 점이다.

```
var person = {
	name: 'Jeong'
};

//delete 연산자를 이용한 프로퍼티 삭제

delete person.name;
console.log(person); //{}
```

쓰지 않도록 하자. 애초에 삭제할 프로퍼티를 만들지 말자!

## 9. ES6에서 추가된 객체 리터럴의 확장 기능

### 9.1 프로퍼티 축약 표현

ES6에서는 프로퍼티 값으로 **변수**를 사용하는 경우 변수의 이름과 프로퍼티 키가 동일한 이름이라면 프로퍼티 키를 생략할수 있다

프로퍼티 키는 변수이름으로 자동 생성

```
//ES5
var x = 1, y = 2;

var obj = {
	x: x,
	y: y
};
console.log(obj);// {x: 1, y: 2}

// ES6에서의 축약 표현

var obj1 = [x,y];

console.log(obj1); // {x: 1, y: 2}
```

### 9.2 계산된 프로퍼티 이름

앞에서, 문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있다고 하였다. 여기서는 대괄호 프로퍼티 접근 연산자를 사용하는데, 표현식에는 계산식이 들어갈 수도 있다.

```
var prefix = 'prop';
var i= 0;

var obj = {};

obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;

console.log(obj) // {prop-1: 1, prop-2: 2, prop-3: 3}

//ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 동적 생성 가능하다.

const prefix = 'prop';
let i = 0;

//객체 리터럴 내부에서 computed property name 으로 프로퍼티 키 생성

const obj = {
	[`${prefix}-${++i}`]: i,
	[`${prefix}-${++i}`]: i,
	[`${prefix}-${++i}`]: i
};

console.log(obj);
//{prop-1: 1, prop-2: 2, prop-3: 3}
```

### 9.3 메서드 축약 표현

ES5 에서 메서드를 표기할 때 프로퍼티 키와 값을 명확히 구분해줬지만 ES 6에서는 축약표현을 사용할 수 있다.

```
//ES5
var coffeeMachine = {
	coffee: 10,
	releaseCoffee : function() {
		this.coffee--;
		console.log(`남은 커피 수는 ${this.coffee}개 입니다`)
	}
}

//ES6
var coffeeMachine = {
	coffee: 10,
	releaseCoffee() {
		this.coffee--;
		console.log(`남은 커피 수는 ${this.coffee}개 입니다`)
	}
}
```
