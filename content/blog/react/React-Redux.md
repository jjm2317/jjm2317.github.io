---
title: React Redux
date: 2020-12-10 07:55:51
category: "react"
draft: false
---

# Redux

- 1205(토) react 스터디준비

- '리액트를 다루는 기술' 참고

**상태 관리 라이브러리**

러덕스는 리액트 상태관리 라이브러리

- 컴포넌트의 상태 업데이트 관련 로직을 다른파일로 분리
- 컴포넌트의 상태 공유시에도 컴포넌트를 거치지 않고 처리
- 전역 상태를 관리할 때 효과적
- 미들웨어를 통한 비동기 작업

## Conceptual overview

### 액션

- 상태에 변화가 필요하면 action이 발생
- 액션은 하나의 객체로 표현

```js
{
  type: "TOGGLE_VALUE";
}
```

- 액션 객체는 type 필드를 반드시 가지고 있어야한다.
  - type은 액션의 이름으로 취급
- 이외의 값은 사용자 임의로 지정

```js
{
    type: 'ADD_TODO',
    data: {
        id: 1,
        text: 'asdf'
    }
}

{
    type: 'CHANGE_INPUT',
    text:'안녕하세요'
}
```

#### 액션 생성 함수(action creater)

- 액션 객체를 만들어 주는 함수

```js
addTodo = (data) => ({ type: "ADD_TODO", data });
```

#### 리듀서(reducer)

- 리듀서는 변화를 일으키는 함수

1. 액션 발생
2. 리듀서가 파라미터로 현재 상태, 액션객체를 받아옴
3. 새로운 상태 반환

```js
const initialState = {
    counter: 1
};
const reducer = (state = initialState, action) {
    switch(action.type) {
        case INCREMENT:
            return {
                counter: state.counter + 1
            };
        default:
            return state;
    }
}
```

#### 스토어(store)

- 프로젝트에 리덕스를 적용하기위해 스토어를 만듬
- 한개의 프로젝트는 하나의 스토어
- 스토어 안에 들어있는 것들
  - 현재 애플리케이션 상태
  - 리듀서
  - 몇가지 내장 함수

#### 디스패치(dispatch)

- 스토어의 내장 함수 중 하나
- 액션을 발생시킨다
- 액션객체를 파라미터로 넣어서 호출

#### 구독(subscribe)

- 스토어의 내장 함수

1. 리스너 함수를 파라미터로 넣어서 호출
2. 액션이 디스패치
3. 상태가 업데이트 될때마다 호출

```js
const listener = () => {
  console.log("상태가 업데이트됨");
};
const unsubscribe = store.subscribe(listener);
```

### Redux without React

리덕스는 리액트에 종속되는 라이브러리가 아니다.

리액트에서 사용하려고 만들어졌지만 다른 라이브러리 / 프레임워크와 함께 사용가능

#### Parcel로 프로젝트 만들기

**Parcel**

- 웹 애플리케이션 프로젝트를 구성할 수 있는도구

```
$ yarn global add parcel-bundler
// or
$ npm install -g parcel-bundler

//html 파일 생성
$ touch index.html
//개발용 서버 실행
$ parcel index.html


```

**index.html**

```html
<html>
  <head>
    <link rel="stylesheet" type="text/css" href="index.css" />
  </head>
  <body>
    <div class="toggle"></div>
    <hr />
    <h1>0</h1>
    <button id="increase">+1</button>
    <button id="decrease">-1</button>
    <script src="./index.js"></script>
  </body>
</html>
```

**index.css**

```css
.toggle {
  border: 2px solid black;
  width: 64px;
  height: 64px;
  border-radius: 32px;
  box-sizing: border-box;
}

.toggle.active {
  background: yellow;
}
```

**index.js**

```js
const divToggle = document.querySelector(".toggle");
const counter = document.querySelector("h1");
const btnIncrease = document.querySelector("#increase");
const btnDecrease = document.querySelector("#decrease");
```

#### 액션 타입과 액션 생성 함수 정의

**액션**

- 프로젝트의 상태에 변화를 일으키는 것
- 액션 이름은 문자열 형태, 주로 대문자로 작성
  - 액션 이름은 고유해야함

```js
const TOGGLE_SWITCH = "TOGGLE_SWITCH";
const INCREASE = "INCREASE";
const DECREASE = "DECREASE";
```

**액션 생성 함수**

- 액션 객체를 만드는 함수
- 액션 객체는 type이 있어야함

```js
const toggleSwitch = () => ({ type: TOGGLE_SWITCH });
const increase = (difference) => ({ type: INCREASE, difference });
const decrease = () => ({ type: DECREASE });
```

#### 초깃값 설정

- 초깃값의 형태는 자유
  - 원시값
  - 객체

```js
const initialState = {
    toggle: false,
    counter: 0;
}
```

#### 리듀서 함수 정의

- 변화를 일으키는 함수
- 파라미터
  - state
  - action

```js
const reducer = (state = initialState, action) {
    switch(action.type) {
        case TOGGLE_SWITCH:
            return {
                ...state,
                toggle:!state.toggle
            };
        case INCREASE:
            return {
                ...state,
                counter: state.counter + action.difference
            };
        case DECREASE:
            return {
                ...state,
                counter: state.counter - 1
            };
        default:
            return state;
    }
}
```

#### 스토어 만들기

```js
import { createStore } from "redux";

//...
const store = createStore(reducer);
```

#### render 함수 만들기

```js
//상태가 업데이트 될때마다 호출
// 이미 html 을 사용하여 만들어진 ui의 속성을 상태에 따라 변경

//...
const render = () => {
  const state = store.getState();

  state.toggle
    ? divToggle.classList.add("active")
    : divToggle.classList.remove("active");

  counter.innerText = state.counter;
};

render();
```

#### 구독하기

```js
//스토어의 상태가 바뀔때마다 render 함수 호출
//스토어의 내장함수 subscribe 사용

//subscribe 함수 파라미터로는 함수객체 전달
//해당 함수 객체가 상태 업데이트 시 호출

const listener = () => {
  console.log("상태가 업데이트 됨");
};

const unsubscribe = store.subscribe(listener);
```

```js
//...
const render = () => {
  const state = store.getState();

  state.toggle
    ? divToggle.classList.add("active")
    : divToggle.classList.remove("active");

  counter.innerText = state.counter;
};

render();

store.subscribe(render);
```

#### 액션 발생시키기

```js
//...
// 액션을 발생시키는 것을 디스패치
//스토어 내장함수 dispatch 사용
//파라미터로 액션객체
divToggle.onclick = () => {
  store.dispatch(toggleSwitch());
};

btnIncrease.onclick = () => {
  store.dispatch(increase(1));
};

btnDecrease.onclick = () => {
  store.dispatch(decrease());
};
```
