---
title: UI CircleProgress
date: 2021-02-08 14:05:44
tags:
---

# 원형 progress bar

## 0%에서 100%의 원 차트

```html
<div class="circle">
  <span class="percentage"></span>
</div>
```

```css
.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;

  background: conic-gradient(#ff0 0% 20%, #f0f 20% 100%);
}
```

## 퍼센트 값 동적 반영하는 원 차트

```html
<div class="circle">
  <span class="percent"></span>
</div>
```

```css
.circle {
  position: relative;
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
.percent {
  background: #fff;
  display: block;
  position: absolute;
  top: 50%;
  left: 50%;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  text-align: center;
  line-height: 50px;
  font-size: 20px;
  transform: translate(-50%, -50%);
}
```

```js
const $circle = document.querySelector(".circle");
const circleProgress = (dom, percent) => {
  dom.style.background = `conic-gradient( #0f9e3e 0% ${percent + "%"}, #ddd ${
    percent + "%"
  } 100%)`;
  dom.firstElementChild.innerHTML = "" + percent;
};
circleProgress($circle, 20);
```

### 한계

원을 투명하게 하지 못해서 가장자리에만 색을 주기가 까다롭다.

## SVG

Scalable Vector Graphics

웹에서 그래픽을 표현하는데 사용된다.

**svg 태그**

html 의 svg요소는 svg 그래픽의 컨테이너로 사용된다.

선, 박스 원, 텍스트, 그래픽 이미지 등을 그리는 여러 메서드를 가진다.

### 속성

**width**

- 직사각형 뷰포트의 디스플레이되는 너비

**height**

- 직사각형 뷰포트의 디스플레이되는 높이
  - 길이, 백분율
  - 좌표계의 높이가 아니다

**preserveAspectRatio**

- svg 조각이 다른 종횡비로 표시될 때 어떻게 변형되어야 하는지
  - none, xMinYMin, xMidYMin, xMaxYMin 등등

**viewBox**

- 현재 svg 조각에 대한 svg 뷰포트 좌표
  - 숫자 리스트
- 상위 요소가 있을 경우 해당 요소 기준으로 컨테이너를 만든다
  - 0 0 200 300 의 경우 0,0 좌표에서 x축으로 200 y축으로 300의 좌표계를 만든다
  - width 가 단위의 기준이됨

**x**

- svg 컨테이너의 디스플레이되는 x 좌표

**y**

- svg 컨테이너의 디스플레이되는 y 좌표

### circle element

**어트리뷰트**

**cx**

- 원의 중심의 x 좌표
  - 단위는 뷰박스 width 기준으로 정해짐

**cy**

- 원의 중심의 y좌표

**r**

- 원의 반지름

#### stroke

모양의 아웃라인을 디자인하는데 사용된다.

**stroke**

- 색깔 지정

**stroke width**

- stroke의 두께

### text element

**어트리뷰트**

**x**

- 텍스트 베이스라인의 x 좌표

**y**

- 텍스트 베이스라인의 y좌표

**dx**

- 자간

**dy**

- 줄간격

**anchor**

- 글자 정렬
- start middle end

### progress circle with svg

**원반지름**

돔요소.r.baseVal.value

**stroke dash array**

점선을 만드는 간격

**stroke dash offset**

점선이 시작하는 위치

```html
<div class="container">
<svg
        class="circleContainer"
        fill="#ff0"
        viewBox="0 0 100 100">
        <circle
        class=""
         stroke="#ccc"
         stroke-width="3.5"
         fill="transparent"
         r="30"
         cx="50"
         cy="50"/>

         </circle>
       <circle
         class="progress"
         stroke="#0f9e3e"
         stroke-width="3.5"
         fill="transparent"
         r="30"
         cx="50%"
         cy="50%"/>
         <text text-anchor="middle" fill="#ccc" dy=".3em" font-size="20" x="50%" y="50%">aa</text>
     </svg>
</div>
```

```css
.container {
  width: 400px;
  height: 400px;
  background-color: #ff0;
}
```

```js
const drawProgress = (dom, percent) => {
  const radius = circleDom.r.baseVal.value;
  var circumference = radius * 2 * Math.PI;

  dom.style.strokeDasharray = `${circumference} ${circumference}`;
  dom.style.strokeDashoffset = `${circumference}`;
  const offset = circumference - (percent / 100) * circumference;
  dom.style.strokeDashoffset = offset;
};
```
