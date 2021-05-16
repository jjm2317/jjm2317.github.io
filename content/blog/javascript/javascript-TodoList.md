---
title: javascript TodoList
date: 2020-11-01 21:04:10
category: "javascript"
draft: false
---

# TODO List

## 1. 막짜다가 망한 코드

```html
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Todo</title>
    <link rel="stylesheet" href="style.css" />
    <script src="main.js" defer></script>
  </head>
  <body>
    <header>
      <h1 class="todo__title">ToDo List</h1>
      <div class="input__container">
        <label for="todo-input" class="a11y-hidden">할일 추가하기</label
        ><input
          id="todo-input"
          class="addInput"
          type="text"
          name="todo"
          placeholder="What to do"
        />
        <button class="addButton">추가</button>
      </div>
    </header>
    <main>
      <ul class="todo__list">
        <h2>할일 목록</h2>
      </ul>
    </main>
  </body>
</html>
```

```javascript
let todos = [
  { id: 1, content: "Javascript", completed: false },
  { id: 2, content: "CSS", completed: true },
  { id: 3, content: "HTML", completed: false },
];

const $todoList = document.querySelector(".todo__list");
const $todoItem = document.createElement("div");
$todoItem.innerHTML = `<li class = "todo__item">
<ul class="info__list"><li class="info__num"></li> <li class="info__content"></li> <li class="info__check">
<input type="checkbox" name="check"></li><li class="info__delete">
<button class="delete-button"}>삭제</button></li>`;
const createItem = ({ id, content, completed }) => {
  const $newItem = $todoItem.cloneNode(true);
  const infoList = $newItem.firstElementChild.firstElementChild.children;
  const $infoNum = infoList[0];
  $infoNum.textContent = id;
  const $infoContent = infoList[1];
  $infoContent.textContent = content;
  const $infoCheck = infoList[2].firstElementChild;
  $infoCheck.setAttribute("checked", `${completed}`);
  return $newItem;
};

const render = () => {
  [...$todoList.children].forEach((item) => {
    $todoList.removeChild(item);
  });
  todos.forEach((item) => {
    $todoList.appendChild(createItem(item));
  });
};
// const modify = () =>{
//   $todoList.innerHTML=
// }
render();

// event
const $addInput = document.querySelector(".addInput");
const $addButton = document.querySelector(".addButton");

//newTodo
const createTodo = (content) => {
  const idList = todos.map((todo) => todo.id);
  const newTodo = {
    id: idList.length ? Math.max(...idList) + 1 : 1,
    content,
    completed: false,
  };
  return newTodo;
};
//추가

$addInput.onkeyup = (e) => {
  if (e.key !== "Enter") return;
  if (!$addInput.value) {
    alert("할 일 입력해");
    return;
  }
  const newContent = e.target.value;
  const newTodo = createTodo(newContent);
  todos.push(newTodo);
  $todoList.append(createItem(newTodo));
  $deleteButton = document.querySelectorAll(".delete-button");
  e.target.value = "";
};
$addButton.onclick = (e) => {
  if (!$addInput.value) {
    alert("할 일 입력해");
    return;
  }
  const newContent = $addInput.value;
  const newTodo = createTodo(newContent);
  todos.push(newTodo);
  $todoList.append(createItem(newTodo));
  $deleteButton = document.querySelectorAll(".delete-button");
  $addInput.value = "";
  $addInput.focus();
};

//삭제
let $deleteButton = document.querySelectorAll(".delete-button");

const deleteItem = (button) => {
  const parentItem = button.parentNode.parentNode.parentNode.parentNode;
  $todoList.removeChild(parentItem);
  const delTodo = parentItem.firstElementChild;
  const delNum = delTodo.firstElementChild.firstElementChild.textContent;
  const delIndex = todos.findIndex((item) => item.id === Number(delNum));

  todos.splice(delIndex, 1);
  let newTodos = [];
  for (let i = 0; i < delIndex; i++) {
    newTodos.push({ ...todos[i] });
  }
  for (let i = delIndex; i < todos.length; i++) {
    newTodos.push({ ...todos[i], ...{ id: { ...todos[i] }.id - 1 } });
  }
  todos = newTodos;
  console.log(todos);
  render();
};

$todoList.onclick = (e) => {
  if (![...$deleteButton].includes(e.target)) return;
  deleteItem(e.target);
  $deleteButton = document.querySelectorAll(".delete-button");
};

// 체크

let $todoCheck = document.querySelectorAll("input[type=checkbox]");
console.log($todoCheck);
$todoList.onchange = (e) => {
  if (![...$todoCheck].includes(e.target)) return;
  console.log(e.target.checked);

  changeCheck(e.target.parentNode.parentNode.firstElementChild.textContent);
  e.target.setAttribute("checked", e.target.checked);
  console.log(todos);

  render();
  // e.target.value=!e.target.value;
  $todoCheck = document.querySelectorAll("input[type=checkbox]");
  $deleteButton = document.querySelectorAll(".delete-button");
};

const changeCheck = (check) => {
  todos = todos.map((item) => {
    return item.id === check
      ? { ...item, ...{ completed: !item.completed } }
      : { ...item };
  });
  $todoCheck = document.querySelectorAll("input[type=checkbox]");
  $deleteButton = document.querySelectorAll(".delete-button");
};
```

```css
@import url(/normalize.css);
@import url(//spoqa.github.io/spoqa-han-sans/css/SpoqaHanSans-kr.css);
@import url(https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css);

*,
*::before,
*::after {
  box-sizing: border-box;
}
html {
  font-size: 10px;
}
body {
  font-size: 1.4rem;
  color: #181818;
  font-family: "Noto Sans KR", sans-serif; /* Noto Sans KR 웹폰트 링크 연결 */
  font-weight: 400;
}
/* 숨김 콘텐츠 */
.a11y-hidden,
legend {
  position: absolute; /*레이어함*/
  width: 1px;
  height: 1px;
  overflow: hidden; /*넘치는 것 감추기*/
  margin: -1px;
  clip-path: polygon(0 0, 0 0, 0 0);
  clip: rect(0 0 0 0);
  clip: rect(0, 0, 0, 0);
}
/* clearfix */
.clearfix::after {
  content: "";
  clear: both;
  display: block;
}
/* header 초기화 */
h1,
h2,
h3 {
  margin: 0;
}
/*ul 초기화 */
ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
/* 앵커 태그 초기화 */
a {
  text-decoration: none;
  color: inherit;
}
/* 버튼 초기화 */
button {
  border: 0;
}

/* 헤더 */

header,
main {
  width: 1100px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: center;
  flex-flow: row wrap;
  height: 200px;
  background-color: #db5628;
}
header .todo__title {
  width: 100%;
  text-align: center;
  background-color: orange;
  height: 150px;
  line-height: 140px;
  font-size: 50px;
}

label[for="todo-input"] {
  background-color: skyblue;
}
.input__container {
  height: 50px;
  width: 100%;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
}
.addInput {
  height: 100%;
}

.addButton {
  height: 100%;
  background-color: #000;
  color: #fff;
  font-weight: bold;
}

/* 메인 */
.todo__item {
  background-color: yellow;
  border: 1px solid black;
}
.todo__item .info__list {
  display: flex;
  flex-flow: row nowrap;
  height: 100px;
  justify-content: flex-start;
}
.info__num {
  font-size: 50px;
  line-height: 100px;
  text-align: center;
  width: 100px;
}
.info__num::after {
  content: "번";
}

.info__num {
  background-color: white;
}
.info__content {
  text-align: center;
  width: 800px;
  font-size: 50px;
  background-color: #abc;
  line-height: 100px;
}

input[type="checkbox"] {
  width: 100px;
  height: 100px;
}

.delete-button {
  width: 100px;
  height: 100px;
  font-size: 40px;
  font-weight: 800;
}
```

## 2. 다시 짠 코드 (함수 분리, 데이터 중심으로 개선)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Todos</title>
    <style>
      .todos {
        list-style-type: none;
        padding: 0;
      }
      .container {
        width: 300px;
        margin: 30px auto;
        background-color: orange;
      }
      .todos > li > label > span {
        display: inline-block;
        width: 130px;
        padding: 0 20px;
      }
      .checked {
        text-decoration: line-through;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <input class = "input-todo"type="text" placeholder="enter todo!" / >
      <button class="add">추가</button>
      <ul class="todos">
        <!-- <li>
      <label>
        <input type="checkbox"/> <span>content</span>
      </label>
      <button class="remove">x</button>
    </li> -->
      </ul>
    </div>
  </body>
  <script>
    let todos = [];
    const $todos = document.querySelector(".todos");
    const $input = document.querySelector(".input-todo");
    const $addButton = document.querySelector(".add");

    const fetchTodos = () => {
      return [
        { id: 1, content: "HTML", completed: false },
        { id: 2, content: "CSS", completed: true },
        { id: 3, content: "Javascript", completed: false },
      ];
    };

    const render = () => {
      $todos.innerHTML = todos
        .map(({ id, content, completed }) => {
          return `<li id ="${id}">
        <label>
          <input type="checkbox" ${completed ? "checked" : ""}/>
        <span>${content}</span>
          </label>
        <button class="remove">X</button></li>`;
        })
        .join("");
    };

    const findId = () => {
      return (
        Math.max(
          ...[
            ...todos.map(({ id }) => {
              return id;
            }),
          ]
        ) + 1
      );
    };

    const addTodo = (content) => {
      todos = [{ id: findId(), content, completed: false }, ...todos];
    };

    const sortTodo = () => {
      todos = todos.sort((a, b) => b.id - a.id);
    };

    const todosCheck = ({ id }) => {
      todos = todos.map((todo) =>
        todo["id"] === +id
          ? { ...todo, ...{ completed: !todo.completed } }
          : { ...todo }
      );
    };

    const deleteTodo = ({ id }) => {
      todos = todos.filter((todo) => todo.id !== +id);
    };

    window.addEventListener("DOMContentLoaded", () => {
      todos = fetchTodos();
      sortTodo();
      render();
    });

    $input.onkeyup = (e) => {
      if (e.key !== "Enter" || $input.value === "") return;
      addTodo(e.target.value);
      $input.value = "";
      render();
    };
    $addButton.onclick = (e) => {
      if ($input.value === "") return;

      addTodo($input.value);
      $input.value = "";
      render();
    };
    $todos.onchange = (e) => {
      if (!e.target.matches("li > label > input")) return;
      const $checkParent = e.target.parentNode.parentNode;
      console.log(e.target.getAttribute("checked"));
      e.target.setAttribute("checked", e.target.checked);
      todosCheck($checkParent);
      console.log(todos);
      console.log(e.target.nextElementSibling);
      e.target.nextElementSibling.style.textDecoration = e.target.checked
        ? "line-through"
        : "";
      // console.log(e.target.getAttribute('checked'));
      // render();
    };
    $todos.onclick = (e) => {
      if (!e.target.matches(".remove")) return;
      const $buttonParent = e.target.parentNode;
      deleteTodo($buttonParent);
      $todos.removeChild($buttonParent);
    };
  </script>
</html>
```
