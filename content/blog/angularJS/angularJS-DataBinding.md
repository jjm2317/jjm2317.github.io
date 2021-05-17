---
title: angularJS DataBinding
date: 2020-12-04 07:40:33
category: "angularJS"
draft: false
---

# AngularJS Data Binding

- 아틀라스네트웍스 SKB 업무를 위한 angularJS 공부

- angularJS 공식문서참조 docs.angularjs.org/guide/

**angularjs의 데이터 바인딩**

angularjs에서의 데이터 바인딩은 모델과 뷰 컴포넌트 사이의 데이터에 대한 자동 동기화이다.

angularjs가 데이터바인딩을 실행하는 방식은 개발자로 하여금 모델을 어플리케이션에서 하나의 신뢰가능한 소스로 취급할 수 있다. 뷰는 항상 모델을 반영한다. 모델이 변할때 뷰는 변화를 반영한다. 그리고 반대도 마찬가지이다.

## 고전적인 템플릿 시스템에서의 데이터바인딩

대부분의 템플릿 시스템들은 **단방향**으로 데이터를 바인딩한다

템플릿과 모델 컴포넌트들을 뷰에 병합한다.

병합이 일어난 후, 모델이나 뷰에 연관된 섹션에서의 변화는 자동적으로 뷰에 반영되지 않는다.

더 안좋은 것은, 사용자가 발생시킨 뷰에대한 모든 변화는 모델에 반영되지 않는다

이것은 개발자가 뷰 => 모델 / 모델 => 뷰 로 지속적으로 동기화하는 코드를 작성해야 한다는 것을 의미한다.

## angularjs templates 에서의 Data binding

**angularjs의 template 시스템**

angularjs 템플릿은 다르게 작동한다.

첫번째로 템플릿이 브라우저에 컴파일된다.

그 컴파일과정은 live view를 생성한다.

뷰에서의 모든 변화는 즉시 모델에 반영된다. 그리고 모델에서의 모든 변화는 뷰로 재전달된다.

모델은 어플리케이션 상태에서 single-source-of-truth 이며, 개발자가 모델을 프로그래밍 하는것을 크게 간소화시켜준다.

뷰를 모델에 대한 instant projection이라고 생각해도 된다.

**controller의 분리**

view 가 단지 모델에 대한 projection이기 때문에, 컨트롤러는 완전히 뷰로부터 분리될 수 있고 컨트롤러는 뷰를 무시한다.
