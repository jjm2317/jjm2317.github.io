---
title: angularJS Overview
date: 2020-12-04 07:06:23
category: "angularJS"
draft: false
---

# AngularJS conceptual overview

- 아틀라스네트웍스 SKB 업무를 위한 angularJS 공부

- angularJS 공식문서참조 docs.angularjs.org/guide/

## AngularJS 핵심 개념

- Template
  - 추가 마크업이 있는 HTML
- Directives
  - 커스텀 어트리뷰트와 요소로 확장된 HTML
- Model
  - view에서 유저에게 보이는 데이터 / 유저가 접촉하는 데이터
- Scope
  - Model 이 저장되는 컨텍스트
  - controller, directives, expressions이 접근할 수 있다.
- Expressions
  - scope 으로부터 변수와 표현식에 접근한다.
- Compiler
  - template을 파싱하고 directives와 expressions 를 인스턴스화 한다.
- Filter
  - 유져에게 보여지는 표현식의 값을 형식화한다.
- View
  - 유저가 보는 것들(DOM)
- Data Binding
  - 모델과 뷰사이의 데이터를 동기화한다.
- Controller
  - view의 business logic
  - business logic이란 데이터 베이스와 유저 인터페이스 사이의 데이터 교환을 처리하는 알고리즘을 지칭한다.
- Dependancy Injection
  - 객체와 함수를 만들고 연결한다.
- Injector
  - dependancy Injection의 컨테이너
- Module
  - injector를 구성하는 컨트롤러, 서비스, 필터, 지시문들을 포함하는 앱의 part를 감싸는 컨테이너
- Service
  - 재사용가능한 view들의 독립적인 business logic

## Example

핵심 개념들의 사용 예시들을 살펴보자

### Data binding

비용을 계산하는 폼 만들기

```html
<div ng-app ng-init="qty=1;cost=2">
  <b>Invoice:</b>
  <div>Quantity: <input type="number" min="0" ng-model="qty" /></div>
  <div>Costs: <input type="number" min="0" ng-model="cost" /></div>
  <div><b>Total:</b> {{qty * cost | currency}}</div>
</div>
```

**Template은**

위 markup 이다. 즉 새로운 markup이다.

AngularJS는 **Compiler로**

Templated의 새로운 마크업들을 파싱한다.

**Scope 에는**

입력한 cost 와 qty 가 저장된다.

**Model은**

저장된 cost와 qty 데이터이다.

**View는**

사용자에게 보여지는 DOM 이다.

**Data binding은**

Model 과 View 사이에서 데이터가 연결되는 것이다.

**Directives는**

첫번째 새로운 마크업들을 지칭한다.

```html
<div ng-app ng-init="qty=1;cost=2"></div>
```

html의 어트리뷰트와 요소에 새로운 행위를 적용한다.

위 코드에서는 ng-app 어트리뷰트를 사용했다

ng-app은 자동적으로 어플리케이션을 실행하는 directive와 연결된다.

angularjs는 input을 위한 directive도 정의한다.

ng-model directive는 인풋값의 데이터를 저장하고 업데이트한다.

**Angular 의 DOM 접근**

Angular에선 커스텀 directive를 사용하여 dom에 접근하도록한다.

새로 만든 인공코드는 테스트하기 까다롭기 때문이다.

**the double curly braces(이중 중괄호)**

```

{{expression | filter}}

```

컴파일러가 이 마크업을 파싱할때, 마크업의 평가값으로 번역한다.

template의 expression은 자바스크립트 스러운 코드 스니펫이다.

- angularjs 로 하여금 변수를 읽고 쓰는 것을 가능하게 한다.

변수들이 전역 변수가 아닌 점에 주목하자.

자바스크립트가 함수레벨 스코프인 것처럼,

angularjs는 표현식에 접근가능한 변수들에 대한 scope를 제공한다

**변수들에 저장되는 값은**

documentation에 나온 model로 불린다.해당 마크업은 예시코드에서 angularjs에게 다음과 같이 명령한다.

- input위젯으로부터 우리가 얻은 데이터를 저장
- 그 데이터들을 곱해라

**filter**

위의 예시코드는 filter를 포함한다.

filter는 유저에게 보여줄 표현식의 값을 형식화 한다.

currency는 숫자를 화폐의 형태의 출력값으로 형식화 한다.

**중요한 점**

angularjs는 live binding을 제공한다.

- 값이 변할때마다 표현식의 값은 자동적으로 재계산되고 dom이 해당 값에 따라 업데이트된다.
- 양방향 데이터 바인딩이라고 한다.

### Controllers

**ui 로직을 더해준다**

기능 추가: 다른 통화 단위로 계산 / 돈 지불

**index.html**

```html
<div ng-app="invoice1" ng-controller="InvoiceController as invoice">
  <b>Invoice:</b>
  <div>
    Quantity: <input type="number" min="0" ng-model="invoice.qty" required />
  </div>
  <div>
    Costs: <input type="number" min="0" ng-model="invoice.cost" required />
    <select ng-model="invoice.inCurr">
      <option ng-repeat="c in invoice.currencies">{{c}}</option>
    </select>
  </div>
  <div>
    <b>Total:</b>
    <span ng-repeat="c in invoice.currencies">
      {{invoice.total(c) | currency:c}} </span
    ><br />
    <button class="btn" ng-click="invoice.pay()">Pay</button>
  </div>
</div>
```

**invoice.js**

```js
angular
  .module("invoice1", [])
  .controller("InvoiceController", function InvoiceController() {
    this.qty = 1;
    this.cost = 2;
    this.inCurr = "EUR";
    this.currencies = ["USD", "EUR", "CNY"];
    this.usdToForeignRates = {
      USD: 1,
      EUR: 0.74,
      CNY: 6.09,
    };

    this.total = function total(outCurr) {
      return this.convertCurrency(this.qty * this.cost, this.inCurr, outCurr);
    };
    this.convertCurrency = function convertCurrency(amount, inCurr, outCurr) {
      return (
        (amout * this.usdToForeignRates[outCurr]) /
        this.usdToForeignRates[inCurr]
      );
    };
    this.pay = function pay() {
      window.alert("Thanks!");
    };
  });
```

위파일은 controller 인스턴스를 생성하는 생성자 함수를 구체화한다.

**controller의 목적**

변수와 함수를 expression과 directives에 내보낸다.

**사용**

controller 코드를 포함한 새파일 뿐만 아니라, html에 **ng-controller**를 추가 하였다.

이 directive는 angularjs에 새로운 InvoiceController가 해당 요소에 대해 directive와 자식요소에대한 권한을 가진다는것을 알린다. InvoiceController as invoice 문법은 angularjs에 컨트롤러를 인스턴스화시키고 현재 스코프에서 변수 invoice에 저장하라고 알린다.

**표현식과 controller**

우리는 또한 페이지의 모든 표현식을 컨트롤러 인스턴스에서 변수들을 읽고 쓸수 있도록 바꾸었다.

- 접두에 invoice. 을 붙였다.

가능한 통화종류들이 컨트롤러에 정의가 되어있고 ng-repeat을 사용하는 template에 추가가 되었다.

컨트롤러가 total 함수를 포함하였다. 우리는 해당 함수의 결과값을 dom에 연결할 수 있다.

**livebinding / ngclick**

위의 바인딩은 live이다. 해당 dom 은 function의 결과값이 바뀔때마다 업데이트 된다.

계산을 지불하는 하는 버튼은 ngClick directive를 사용한다. 이것은 연결된 표현식을 버튼이 클릭될때마다 실행한다.

**module의 생성**

새 자바스크립트 파일에서 우리는 컨트롤러를 등록한곳에 모듈을 생성할것이다. 이것에 대해서는 다음 섹션에서 다룬다.

**컨트롤러의 도입후**

### Services

**View-independent business logic**

**service를 통한 로직 분리**

이제 InvoiceController는 우리 예시의 모든 로직을 포함한다.

어플리케이션이 커진다면 view에 독립적인 로직을 컨트롤러에서 service로 옮기는 것은 좋은 행위이다.

그렇게 하면 그 로직은 어플리케이션 다른부분에서도 재사용할 수 있다.

이후에, 우리는 또한 그 service를 controller를 수정하지 않고 웹으로부터 환율을 로드하도록 바꿀수도 있다.

우리의 예시를 refactor해보자.

**index.html**

```html
<div ng-app="invoice2" ng-controller="InvoiceController as invoice">
  <b>Invoice:</b>
  <div>
    Quantity: <input type="number" min="0" ng-model="invoice.qty" required />
  </div>
  <div>
    Costs: <input type="number" min="0" ng-model="invoice.cost" required />
    <select ng-model="invoice.inCurr">
      <option ng-repeat="c in invoice.currencies">{{c}}</option>
    </select>
  </div>
  <div>
    <b>Total:</b>
    <span ng-repeat="c in invoice.currencies">
      {{invoice.total(c) | currency:c}} </span
    ><br />
    <button class="btn" ng-click="invoice.pay()">Pay</button>
  </div>
</div>
```

---

**finance2.js**

```js
angular.module("finance2", []).factory("currencyConverter", function () {
  var currencies = ["USD", "EUR", "CNY"];
  var usdToForeignRates = {
    USD: 1,
    EUR: 0.74,
    CNY: 6.09,
  };
  var convert = function (amount, inCurr, outCurr) {
    return (amount * usdToForeignRates[outCurr]) / usdToForeignRates[inCurr];
  };

  return {
    currencies: currencies,
    convert: convert,
  };
});
```

**invoice2.js**

```js
angular.module("invoice2", ["finance2"]).controller("InvoiceController", [
  "currencyConverter",
  function InvoiceController(currencyConverter) {
    this.qty = 1;
    this.cost = 2;
    this.inCurr = "EUR";
    this.currencies = currencyConverter.currencies;

    this.total = function total(outCurr) {
      return currencyConverter.convert(
        this.qty * this.cost,
        this.inCurr,
        outCurr
      );
    };
    this.pay = function pay() {
      window.alert("Thanks!");
    };
  },
]);
```

**controller의 함수/변수를 service로 분리**

우리는 convertCurrency 함수와 존재하는 통화들의 대한 정의를 finance2.js라는 새로운 파일에 옮겼다.

하지만 어떻게 controller는 이제는 분리된 함수를 붙잡고 있을까?

**Dependency Injection의 의미와 angular에서의 사용**

이것은 Dependency Injection(의존성 주입)이 작용하는 부분이다.

의존성 주입은 소프트웨어 디자인 패턴이다.

- 객체와 함수가 생성되는 방식을 처리한다.
- 객체와 함수들이 그들의 dependencies를 붙잡는 방식을 처리한다.

angularjs의 모든 것들(directives, filters, controllers, services, ...) 는 의존성 주입을 통해 생성되고 연결된다.

angularjs에서, DI container는 **injector**라고 불린다.

**DI(Dependency Injection)의 사용과 module**

DI를 사용하기 위해서, 모든것들이 함께 작용할 공간이 등록되는 것이 필요하다.

angularjs에선, 모듈을 목적으로 한다.

angularjs가 시작할때, ng-app으로 정의된 이름으로 모듈의 구성을 사용한다.

ng-app directive는 모듈이 의존하고 있는 모든 모듈의 구성을 포함한다.

**템플릿의 메인모듈과 의존성 주입을 통한 서비스 제공**

위 예제에서는 템플릿은 ng-app="invoice2" 디렉티브를 포함한다.

이 디렉티브는 angularjs 에게 invoice2 모듈을 어플리케이션의 메인 모듈로 사용하라고 말한다.

코드 스니펫 angular.module('invoice2', ['finance2']) 는 invoice2 모듈이 finance2 모듈에 의존하고 있다는 것을 구체화한다.

이것으로, angularjs는 InvoiceController를 currencyConverter service에 추가로 사용한다.

**service 가 생성되는 방식**

angularjs가 어플리케이션의 모든 parts를 알게 되었으므로, 그것들을 생성해야한다.

이전 섹션에서는 우리는 컨트롤러들이 생성자 함수를 통해 생성되는것을 보았다.

service들은 생성되는 여러가지 방식들이 있다.

위 예제에서는, currencyConverter service에 대한 factory functiond으로 무기명 함수를 사용하였다.

이 함수는 currencyConverter 의 service 인스턴스를 반환해야한다.

**상위 모듈의 식별자를 참조하는 방법**

어떻게 InvoiceController는 currencyConverter 함수에 대한 참조를 얻을 수 있을까?

Angularjs 에서는, 생성자함수에 인수로 정의 하는방식으로 진행된다.

이것으로, injector는 올바른 순서로 객체를 생성하고 이전에 생성된 객체를 객체의 factories로 보낼수있다.

invoice2.js

```js
angular.module('invoice2', ['finance2'])
.controller('InvoiceController', ['currencyConverter', function InvoiceController(currencyConverter) ...
```

우리의 예시에서 InvoiceController는 currentConverter 라는 인수를 가지고 있다.

이것으로, angularjs는 controller와 service간의 의존성을 알게되고 controller를 service인스턴스와 함께 호출할 수 있다.

**controller에 배열로 인수전달**

이전 섹션과 지금 섹션에서의 차이점 중 마지막 항목은 modul.controller에 일반 함수대신 배열을 전달한 것이다.

invoice2.js

```js
angular.module('invoice2', ['finance2'])
.controller('InvoiceController', ['currencyConverter', function InvoiceController(currencyConverter) ...
```

invoice1.js

```js
angular.module('invoice1', [])
.controller('InvoiceController',
function InvoiceController(){....
```

배열의 첫 요소에는 controller가 사용할 service의 이름이 들어간다. 마지막 요소에는

controller 생성자 함수가 들어간다.

Angularjs는 이 배열을 사용해서 dependencies를 정의한다.

이렇게 함으로서 Dependencies Injection은 코드를 간소화 한 후에도 작용한다.

### Accessing the backend
