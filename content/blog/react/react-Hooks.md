---
title: react Hooks
date: 2020-11-14 13:42:17
category: "react"
draft: false
---

# 리액트 Hooks 발표자료

**목차**

- Hooks란?

- useState

- useEffect

- useReducer

- useMemo

- useCallback

- useRef

**Hooks란**

- 리액트 패키지에서 제공하는 함수들
  - 각 함수를 hook이라고 하며 특정한 기능을 구현하는데 쓰임

**함수형 컴포넌트의 사용**

- Hooks가 도입되기 전에는 함수형 컴포넌트에서 state를 통한 상태관리를 할 수 없었다.

  - 클래스에서는 Component를 가져와 state를 사용하는 것이 가능했지만 함수형은 지원되는 기능이 없었다.

- Hooks 도입후 useState, useEffect 등으로 상태관리 등의 다양한 작업이 가능해졌다.

- 즉 클래스형 컴포넌트의 기능을 사용할 수 있는 함수형 컴포넌트를 Hooks를 통해구현 가능하다.

**장점**

- 함수의 재사용 가능
- 클래스형 컴포넌트에 비해 가독성이 좋다
  - 클래스형 컴포넌트는 로직이 한 곳에 모여있음
  - 함수형 컴포넌트는 로직을 분리시킨 후 조립하는 형태

## 1. useState

- 가장 기본적인 Hook

- 상태관리

**useState의 기능**

함수형 컴포넌트에서도 상태관리를 가능하게 하여 가변적인 상태를 지닐 수 있게 해준다. 즉 상태관리할 때 useState 사용

**사용법**

```react
import React, {useState} from 'react';

const f = () => {
	const[state, setState] = useState('init')

    // ...
}
```

**예제1 - **Counter.js

```react
//리액트 패키지에서 useState 훅 가져오기
import React, {useState} from 'react';

//함수형 컴포넌트 작성
const Counter = () => {
  //useState함수는 배열을 반환
	//배열 비구조화 할당으로 변수 선언
  //[상태 값, 상태를 설정하는 함수]
  //useState(상태의 기본값, 즉 value의 초기값)
  const [value, setValue] = useState(0)

  //JSX 반환문
  //버튼을 클릭 시 value를 증가시키기
  //이벤트 핸들러 어트리뷰트 방식
  return (
    <div>
      <p>{value}</p>
      <button onClick = {()=> setValue(value +1)}>증가</button>
    </div>
  )
}

export default Counter;
```

**useState 여러번 사용**

```react
//리액트 패키지에서 useState 훅 가져오기
import React, { useState } from "react";

//함수형 컴포넌트 작성
const Counter = () => {
  //useState호출하여 상태를 나타내는 변수 선언
  const [value, setValue] = useState(0);
  const [value2, setValue2] = useState("체크");
  //JSX 반환문
  //버튼을 클릭 시 value를 증가시키기
  return (
    <div>
      <p>{value}</p>
      <button onClick = {()=>setValue(value+1)}>증가</button>
      <p>{value2}</p>
      <input type="checkbox" onChange = {e => setValue2(e.target.checked?'체크됨' : '체크안됨')}/>
    </div>
  );
};

export default Counter;
```

## 2. useEffect

- 리액트 컴포넌트가 렌더링 될때마다 특정 작업을 수행하도록 설정할 수 있는 Hook

- useState가 상태를 초기화, 변화시켰다면 useEffect는 상태변화를 감지
  - 마운트(렌더링 직후)를 감지
  - 업데이트(상태의 변화) 를 감지
- 첫 번째에는 콜백함수, 두번째로는 배열 전달

**사용법**

```
import React, {useState, useEffect} from 'react';

const f = () =>{
	const [value, setValue] = useState('init')

	useEffect(()=>{}, [value])
}
```

**내 예제: useEffect 마운트 , 업데이트 감지**

```react
import React, { useState } from "react";

//함수형 컴포넌트 작성
const Counter = () => {
  //useState
  const [value, setValue] = useState(0);
  const [value2, setValue2] = useState("체크안됨");
  //useEffect 호출 : 마운트, 업데이트 감지
    useEffect(()=>{
        console.log('렌더링 완료',value, value2)
    })
  return (
    <div>
      <p>{value}</p>
      <button onClick = {()=>setValue(value+1)}>증가</button>
      <p>{value2}</p>
      <input type="checkbox" onChange = {e => setValue2(e.target.checked?'체크됨' : '체크안됨')}/>
    </div>
  );
};

export default Counter;
```

**useEffect 마운트만 감지**

```react
import React, { useState } from "react";

//함수형 컴포넌트 작성
const Counter = () => {
  //useState
  const [value, setValue] = useState(0);
  const [value2, setValue2] = useState("체크안됨");
  //useEffect 호출 : 마운트만 감지
  //두번째 인수로 빈배열 전달
    useEffect(()=>{
        console.log('렌더링 완료', value, value2);
    },[])
  return (
   // ...
  );
};

export default Counter;
```

**useEffect 특정 값 업데이트만 감지**

```react
import React, { useState } from "react";

//함수형 컴포넌트 작성
const Counter = () => {
  //useState
  const [value, setValue] = useState(0);
  const [value2, setValue2] = useState("체크안됨");
  //useEffect 호출 : 마운트, 특정 값 업데이트 감지
  //두번째 인수로 준 빈배열에 해당 state입력
    useEffect(()=>{
        console.log('렌더링 완료', value, value2);
    },[value])
  return (
   // ...
  );
};

export default Counter;
```

**useEffect 뒷정리**

- 기본적으로 업데이트 직전에 뒷정리 함수가 호출

```react
useEffect(()=>{
        console.log('렌더링 완료', value, value2);
    	return ()=>console.log('업데이트 전');
    });
```

- 컴포넌트의 언마운트 직전에도 호출

```react
useEffect(()=>{
        console.log('렌더링 완료', value, value2);
    	return ()=>console.log('언마운트 전');
    });
// ......
// App.js
import React, { useState } from "react";
import Counter from "./Counter";

const App = () => {
  const [checked, setChecked] = useState(false);
  return (
    <div>
      <label key="check">보이기<input id ="check"type = "checkbox"onChange ={e => setChecked(e.target.checked)}/></label>
      {checked?<Counter /> : <b>닫힘</b>}
    </div>
  );
};

export default App;

```

- 언마운트 직전에만 호출하고 싶다면

```
//두번쩨 인수에 빈배열 전달
useEffect(()=>{
        console.log('렌더링 완료', value, value2);
    	return ()=>console.log('언마운트 전');
    },[]);
```

**책 예제**: Info.js

```react
import React, {useState, useEffect} from 'react';

const Info = () => {
  //useState로 상태 기본값 설정
  const [name, setName] = useState('');
  const [nickname, setNickname]= useState('');
  //useEffect: 마운트(렌더링 직후)를 감지, 업데이트(상태변화)를 감지
  useEffect(() => {
    console.log('렌더링이 완료되었습니다!');
    console.log({
      name,
      nickname
    });
    return ()=>console.log('언마운트 직전');
  },[]);

  //이벤트 핸들러 함수 선언
  const onChangeName = e => {
    setName(e.target.value);
  };

  const onChangeNickname = e => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange = {onChangeName}/>
        <input value={nickname} onChange={onChangeNickname}/>
      </div>
      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임:</b> {nickname}
        </div>
      </div>
    </div>
  )
}

export default Info;
```

**책예제: App.js**

```react
import React, { useState } from "react";
import Info from "./Info";

const App = () => {
  const [checked, setChecked] = useState(false);
  return (
    <div>
      <label for="check">보이기<input id ="check"type = "checkbox"onChange ={e => setChecked(e.target.checked)}/></label>
      {checked?<Info /> : <b>닫힘</b>}
    </div>
  );
};

export default App;

```

## 3. useReducer

- 상태관리 함수
- useState보다 더 다양한 컴포넌트 상황에 따라 다양한 상태를 다른값으로 업데이트 해주고 싶을때 사용
- 리듀서 함수에서 새로운 상태를 만들때는 불변성을 지켜야함

**사용법**

- useReducer의 첫 번째 파라미터에 리듀서 함수, 두번째 파라미터에 해당 리듀서의 기본값
- state : 현재 가리키고 있는 상태
- dispatch: 액션을 발생시키는 함수

**책 예제: CounterReducer**

```react
import React, {useReducer} from 'react';
//리듀서 함수 정의

function reducer(state, action){
	switch(action.type){
		case 'INCREMENT':
			return{ value: state.value + 1};
        case 'DECREMENT' :
            return{ value: state.value -1 };
        default:
            return state;
	}
}

const Counter = () => {
    const [state, dispatch] = useReducer(reducer, {value: 0});

    return(
    	<div>
        	<p>
            	현재 카운터 값 : {state.value}
            </p>
            <button onClick= {()=>dispatch({type: 'INCREMENT'})}>
                +1
            </button>
            <button onClick= {()=>dispatch({type: 'DECREMENT'})}>
                -1
            </button>
        </div>
    )
}
export default Counter;
```
