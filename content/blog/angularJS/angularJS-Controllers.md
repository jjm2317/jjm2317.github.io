---
title: angularJS Controllers
date: 2020-12-10 07:56:29
category: "angularJS"
draft: false
---

# Controllers

- SKB 업무를 위한 라이브러리 공부
- AngularJS 공식문서 참조

## Controller란

**controller의 개념과 쓰임**

- AngularJS 에서 controller는 스코프를 추가하는 생성자 함수에 의해 정의 된다.
- 컨트롤러는 여러 방법으로 dom에 연결될 수 있다.
- 새로운 controller 객체는 컨트롤러 생성자 함수를 사용하여 인스턴스화 된다.

**controller 종류**

- ngController directive
  - 새로운 child 스코프가 생성되고 사용가능해진다.
  - child 스코프는 컨트롤러의 매개변수로 주입되면 사용가능하다.

**controller as**

컨트롤러가 controller as 문법을 사용하게 되면 컨트롤러 인스턴스는 스코프의 프로퍼티로 할당된다.

**사용**

컨트롤러는 다음과 같이 사용된다.

- $scope 객체의 초기 상태 설정
- $scope 객체에 행위 추가

**다음과 같은 사용은 지양**

- DOM 조작
  - 컨트롤러는 비지니스 로직만을 포함해야한다.
  - 시각적으로 보여지는 로직을 넣는 것은 검증가능성에 영향을 준다.
  - angularJS는 대부분의 경우 데이터 바인딩을 갖는다.
  - 수동적인 돔조작을 위한 디렉티브를 갖는다.
- input 구성
  - AngularJS form control 사용
- filter
  - AngularJS filter사용
- 컨트롤러간의 코드 / 상태 공유
  - AngularJS services 사용
- 다른 컴포넌트의 생명주기 관리

**정리**

일반적으로 Controller는 많은 것을 수행하면 안된다.

하나의 single view 에 필요한 비지니스 로직만을 포함해야한다.

**way to keep controller slim**

- 컨트롤러레 속하지 않는 작업들을 services로 묶는다
- dependency injection 으로 services 들을 Controller 에서 사용한다.

## $scope Object의 초깃값 설정

**$scope의 initial state**

- $scope 객체에 프로퍼티를 추가하여 초깃값 세팅한다.
- 프로퍼티는 view model을 포함한다.
- 모든 $scope 프로퍼티는 해당 컨트롤러가 등록된 dom이 있는 템플릿에 사용 가능하다.

### 예시

**GreetingController 생성**

```js
const myApp = angular.module("myApp", []);

myApp.controller("GreetingController", [
  "$scope",
  function ($scope) {
    $scope.greeting = "Hola!";
  },
]);
```

1. AngularJS Module myApp 생성
2. 모듈에 controller 메서드로 컨트롤러 생성자 함수 추가
   - 컨트롤러 생성자 함수가 전역 스코프를 벗어나게 해준다.

**inline injection annotation**

1. angularJS 로부터 $scope service를 제공받는다.
2. 해당 $scope에 컨트롤러의 dependency를 구체화한다.

**3. DOM 요소에 directive 추가**

```html
<div ng-controller="GreetingController">{{ greeting }}</div>
```

## Scope 객체에 행위 추가

### 동작을 컨트롤 하는 방법

**이벤트 핸들링 or 계산**

- view에서 이벤트에 반응하거나 계산을 수행해야 한다.
  - scope에 behavior를 제공
  - behavior는 $scope 객체에 메서드를 정의하는 방식으로 추가
  - 해당 메서드는 템플릿/뷰 에서 호출하는 방식으로 사용된다.

### 예시

**숫자를 2 곱하는 메서드를 스코프에 추가**

```js
const myApp = angular.module("myApp", []);

myApp.controller("DoubleController", [
  "$scope",
  function ($scope) {
    $scope.double = (value) => value * 2;
  },
]);
```

**템플릿에서 사용**

- AngularJS 표현식에서 호출되어 사용된다

```html
<div ng-controller="DoubleController">
  Two times <input ng-model="num" /> equals {{ double(num) }}
</div>
```

**스코프에 할당된 프로퍼티**

스코프에 프로퍼티로 추가된 모든 객체는 model의 프로퍼티가 된다.

스코프에 추가된 모든 메서드들은 템플릿 / 뷰에서 사용 가능하다.

EX

- 표현식에서의 사용
- 이벤트 핸들러 디렉티브에서의 사용

## Simple Spicy Controller Example

### Controller 이해를 위한 간단한 앱 만들기

**앱의 구성**

- 두개의 버튼과 하나의 간단한 메시지가 있는 template
- spice로 명명된 문자열을 포함하는 model
- spice의 값을 설정하는 두개의 함수가 있는 컨트롤러

**index.html**

```html
<div ng-controller="SpicyController">
  <button ng-click="chiliSpicy()">Chili</button>
  <button ng-click="jalapenoSicy()">Jal</button>
  <p>The food is {{spice}} spicy</p>
</div>
```

**app.js**

```js
const myApp = angular.module("spicyApp", []);

myApp.controller("SpicyController", [
  "$scope",
  function ($scope) {
    $scope.spice = "very";

    $scope.chiliSpicy = () => {
      $scope.spice = "chili";
    };

    $scope.jalSpicy = () => {
      $scope.spice = "jalapeno";
    };
  },
]);
```

- ng-contorller 디렉티브는 템플릿에 스코프를 생성하는데 쓰임
- 위 예제의 spicyController는 일반 함수이다. 파스칼표기법으로 표기
- $scope 프로퍼티를 전달하는 것은 모델을 업데이트
- 컨트롤러 메서드는 스코프에 메서드를 추가하면서 생성
