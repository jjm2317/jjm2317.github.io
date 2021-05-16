---
title: javascript restAPI&TodoList
date: 2020-11-10 23:50:38
category: "javascript"
draft: false
---

# REST API 로 TodoList 구현

## todos.js (saved in ./data)

```
const todos = [
  { id: 1, content: 'HTML', completed: false },
  { id: 2, content: 'CSS', completed: true },
  { id: 3, content: 'Javascript', completed: false },
].sort((t1, t2) => t2.id - t1.id);

exports.todos = todos;

```

## index.html

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Todos 4.0</title>
  <link href="css/style.css" rel="stylesheet">
  <script defer src="js/app.js"></script>
</head>
<body>
  <div class="container">
    <h1 class="title">Todos</h1>
    <div class="ver">4.0</div>

    <input class="input-todo" placeholder="What needs to be done?" autofocus>
    <ul class="nav">
      <li id="all" class="active">All</li>
      <li id="active">Active</li>
      <li id="completed">Completed</li>
    </ul>
    <ul class="todos">
      <!-- <li id="myId" class="todo-item">
        <input id="ck-myId" class="checkbox" type="checkbox">
        <label for="ck-myId">HTML</label>
        <i class="remove-todo far fa-times-circle"></i>
      </li> -->
    </ul>
    <footer>
      <div class="complete-all">
        <input class="checkbox" type="checkbox" id="ck-complete-all">
        <label for="ck-complete-all">Mark all as complete</label>
      </div>
      <div class="clear-completed">
        <button class="btn">Clear completed (<span class="completed-todos">0</span>)</button>
        <strong class="active-todos">0</strong> items left
      </div>
    </footer>
  </div>
</body>
</html>

```

## style.css

```
@import url('https://fonts.googleapis.com/css?family=Roboto:100,300,400,700%7CNoto+Sans+KR');
@import url('https://use.fontawesome.com/releases/v5.5.0/css/all.css');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Roboto', 'Noto Sans KR', sans-serif;
  font-size: 0.9em;
  color: #58666E;
  background-color: #F0F3F4;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.container {
  max-width: 750px;
  min-width: 450px;
  margin: 0 auto;
  padding: 15px;
}
.title {
  /* margin: 10px 0; */
  font-size: 4.5em;
  font-weight: 100;
  text-align: center;
  color: #23B7E5;
}
.ver {
  font-weight: 100;
  text-align: center;
  color: #23B7E5;
  margin-bottom: 30px;
}
/* .input-todo  */
.input-todo {
  display: block;
  width: 100%;
  height: 45px;
  padding: 10px 16px;
  font-size: 18px;
  line-height: 1.3333333;
  color: #555;
  border: 1px solid #ccc;
  border-color: #E7ECEE;
  border-radius: 6px;
  outline: none;
  transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;
}
.input-todo:focus {
  border-color: #23B7E5;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.input-todo::-webkit-input-placeholder {
  color: #999;
}
/* .nav */
.nav {
  display: flex;
  margin: 15px;
  list-style: none;
}
.nav > li {
  padding: 4px 10px;
  border-radius: 4px;
  cursor: pointer;
}
.nav > li.active {
  color: #fff;
  background-color: #23B7E5;
}
.todos {
  margin-top: 20px;
}
/* .todo-item */
.todo-item {
  position: relative;
  /* display: block; */
  height: 50px;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-color: #E7ECEE;
  list-style: none;
}
.todo-item:first-child {
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}
.todo-item:last-child {
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
}
/*
  .checkbox
  .checkbox 바로 뒤에 위치한 label의 before와 after를 사용해
  .checkbox의 외부 박스와 내부 박스를 생성한다.
  <input class="checkbox" type="checkbox" id="myId">
  <label for="myId">Content</label>
*/
.checkbox {
  display: none;
}
.checkbox + label {
  position: absolute; /* 부모 위치를 기준으로 */
  top: 50%;
  left: 15px;
  transform: translate3d(0, -50%, 0);
  display: inline-block;
  width: 90%;
  line-height: 2em;
  padding-left: 35px;
  cursor: pointer;
  user-select: none;
}
.checkbox + label:before {
  content: "";
  position: absolute;
  top: 50%;
  left: 0;
  transform: translate3d(0, -50%, 0);
  width: 20px;
  height: 20px;
  background-color: #fff;
  border: 1px solid #CFDADD;
}
.checkbox:checked + label:after {
  content: "";
  position: absolute;
  top: 50%;
  left: 6px;
  transform: translate3d(0, -50%, 0);
  width: 10px;
  height: 10px;
  background-color: #23B7E5;
}
/* .remove-todo button */
.remove-todo {
  display: none;
  position: absolute;
  top: 50%;
  right: 10px;
  cursor: pointer;
  transform: translate3d(0, -50%, 0);
}
/* todo-item이 호버 상태이면 삭제 버튼을 활성화 */
.todo-item:hover > .remove-todo {
  display: block;
}
footer {
  display: flex;
  justify-content: space-between;
  margin: 20px 0;
}
.complete-all, .clear-completed {
  position: relative;
  flex-basis: 50%;
}
.clear-completed {
  text-align: right;
  padding-right: 15px;
}
.btn {
  padding: 1px 5px;
  font-size: .8em;
  line-height: 1.5;
  border-radius: 3px;
  outline: none;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
  cursor: pointer;
}
.btn:hover {
  color: #333;
  background-color: #E6E6E6;
  border-color: #ADADAD;
}
```

## app.js

```
//variables
const $todos = document.querySelector('.todos');
const $inputTodo = document.querySelector('.input-todo');
const $completeAll = document.getElementById('ck-complete-all');
const $clearButton = document.querySelector('.btn');
const $completedTodos = document.querySelector('.completed-todos')
const $activeTodos = document.querySelector('.active-todos');
const $nav = document.querySelector('.nav');


// const $checkBox = document.querySelector('.checkbox');
let todos = [];



// fetch
const request = {
  get(url) {
    return fetch(url);
  },
  post(url, payload) {
    return fetch(url,{
      method: 'POST',
      headers: {'content-Type': 'application/json'},
      body: JSON.stringify(payload)
    });
  },
  patch(url, payload) {
    return fetch(url, {
      method: 'PATCH',
      headers: {'content-Type' : 'application/json'},
      body: JSON.stringify(payload)
    });
  },
  delete(url) {
    return fetch(url, {method: 'DELETE'});
  }
};


// function
// 렌더링 함수
const render = () => {
// 탭에 따른 렌더링 변화를 주기 위해 복사본에 조건에 맞는 값 할당 후 해당 복사본 렌더링
  let _todos = [];
  const $active = document.querySelector('.active');
  $active.matches('#all') ? _todos = todos : ($active.matches('#active') ?
  _todos = todos.filter(todo=> !todo.completed) :
  _todos = todos.filter(todo => todo.completed))

  // todos 렌더링
   $todos.innerHTML =
  _todos.map(todo => {
   return `<li id="${todo.id}" class="todo-item">
  <input id="ck-${todo.id}" class="checkbox" type="checkbox" ${todo.completed ? 'checked' : ''}>
  <label for="ck-${todo.id}">${todo.content}</label>
  <i class="remove-todo far fa-times-circle"></i>
</li>`}).join('');

// 하단 완료개수, 남은 할일 개수 표시
    $completedTodos.textContent = todos.filter(todo => todo.completed).length
    $activeTodos.textContent = todos.filter(todo => todo.completed === false).length
}



// event
window.onload = () => {
  request.get('/todos')
  .then(_todos => _todos.json())
  .then(_todos => {todos = _todos} )
  .then(render)
  .catch(err => console.error(err));

}
// todo 입력 및 추가
$inputTodo.onkeyup = e => {
  if(e.key !== 'Enter') return;
  request.post('/todos',{
    id : todos.length ? Math.max(...todos.map(todo=>todo.id)) + 1 : 1,
    content: e.target.value
    ,completed: false})
  .then(response => response.json())
  .then(_todos => todos = _todos)
  .then(render)
  .catch(err => console.error(err));
}

// todo 체크박스 체크
$todos.onchange = e => {
  console.log(e.target.id);
  request.patch(`/todos/${e.target.parentNode.id}`,{
    completed : e.target.checked
  })
  .then(response => response.json())
  .then(_todos => {todos = _todos})
  .then(render)
  .catch(err => console.error(err));
}

// 체크박스 전부 완료표시
$completeAll.onchange = e => {
  request.patch('/todos/completed',{
    completed: e.target.checked ? true : false
  })
  .then(response => response.json())
  .then(_todos => todos = _todos)
  .then(render)
  .catch(err => console.error(err));
}

// 완료목록 삭제
$clearButton.onclick = e => {
  request.delete(`/todos/completed`)
  .then(response => response.json())
  .then(_todos => todos = _todos)
  .then(render)
  .catch(err => console.error(err));
}

// 탭 클릭시 활성화 변화
$nav.onclick = e => {
  if(!e.target.matches('.nav li')) return;
  [...$nav.children].forEach(item => {
    item.classList.toggle('active',e.target === item);
  });
  render();
}

```

## server.js

```
const express = require('express');
const cors = require('cors');

let { todos } = require('./data/todos');

const app = express();

app.use(cors());
app.use(express.static('public'));
app.use(express.json()); // for parsing application/json

app.get('/todos', (req, res) => {
  res.send(todos);
});

app.get('/todos/:id', (req, res) => {
  res.send(todos.filter(todo => todo.id === +req.params.id));
});

app.post('/todos', (req, res) => {
  const newTodo = req.body;

  if (!Object.keys(newTodo).length) {
    return res.send({
      error: true,
      reason: '페이로드가 없습니다. 새롭게 생성할 할일 데이터를 전달해 주세요.',
    });
  }

  if (todos.map(todo => todo.id).includes(newTodo.id)) {
    return res.send({
      error: true,
      reason: `${newTodo.id}는 이미 존재하는 id입니다.`,
    });
  }

  todos = [newTodo, ...todos];
  res.send(todos);
});

// 모든 할일의 completed를 일괄 변경
app.patch('/todos/completed', (req, res) => {
  const completed = req.body;

  todos = todos.map(todo => ({ ...todo, ...completed }));
  res.send(todos);
});

app.patch('/todos/:id', (req, res) => {
  const id = +req.params.id;
  const completed = req.body;

  if (!todos.map(todo => todo.id).includes(id)) {
    return res.send({
      error: true,
      reason: `id가 ${id}인 할일 데이터가 존재하지 않습니다.`,
    });
  }

  todos = todos.map(todo =>
    todo.id === id ? { ...todo, ...completed } : todo
  );
  res.send(todos);
});

// completed가 true인 모든 할일 데이터 삭제
app.delete('/todos/completed', (req, res) => {
  todos = todos.filter(todo => !todo.completed);
  res.send(todos);
});

// 아래 라우터를 DELETE '/todos/completed'보다 앞에 위치시키려면 url을 '/todos/:id([0-9]+)'로 변경한다.
app.delete('/todos/:id', (req, res) => {
  const id = +req.params.id;

  if (!todos.map(todo => todo.id).includes(id)) {
    return res.send({
      error: true,
      reason: `id가 ${id}인 할일 데이터가 존재하지 않습니다.`,
    });
  }

  todos = todos.filter(todo => todo.id !== id);
  res.send(todos);
});

app.listen('7000', () => {
  console.log('Server is listening on http://localhost:7000');
});
```
