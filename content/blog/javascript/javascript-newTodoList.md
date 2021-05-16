---
title: javascript newTodoList
date: 2020-11-02 16:18:48
category: "javascript"
draft: false
---

# TodoList 과제

```
// State
let todos = [];
let data = [];
const $todos = document.querySelector('.todos');
const $input = document.querySelector('.input-todo');
const $addButton = document.querySelector('.add');
const $filter = document.querySelector('.nav');
const $clear = document.querySelector('.clear-completed');
const $todoCompleted = document.querySelector('.completed-todos');
const $todoActive = document.querySelector('.active-todos');
const $completeAll = document.querySelector('#ck-complete-all');
const fetchTodos = () => {
  return  [
{ id: 1, content: 'HTML', completed: false },
{ id: 2, content: 'CSS', completed: true },
{ id: 3, content: 'Javascript', completed: false }
]
};

const render = () => {
  $todos.innerHTML = todos.map(({id, content, completed}) => {
      return `<li id="${id}" class="todo-item">
      <input id="ck-${id}" class="checkbox" type="checkbox" ${completed ? "checked" : ''}>
      <label for="ck-${id}">${content}</label>
      <i class="remove-todo far fa-times-circle"></i>
    </li>`
  }).join('');
  $todoCompleted.textContent = todos.filter(todo => todo.completed === true).length;
  $todoActive.textContent = todos.filter(todo => todo.completed === false).length;
}
const updateData = () =>{
  data = data.map(todo => {
    const test = todos.find(item => todo.id === item.id);
    return test ? {...todo, ...test} : {...todo}
  })
}
const findId = () => {
  return Math.max(...todos.map(({id}) => id),0)+1;
  updateData()
}

const addTodo = (content) => {
  const newTodo = {id: findId(), content, completed: false}
  todos = [newTodo, ...todos];

  data = [newTodo,...data];
  updateData()
  console.log(todos,data);
}

const sortTodo = () => {
  todos = todos.sort((a, b) => b.id - a.id)
  // updateData()
}

const todosCheck = ({id}) => {
  todos = todos.map(todo => todo['id'] === +id ? {...todo,...{completed: !todo.completed}} : {...todo});
}
const filterActiveCheck = () => {
  todos = todos.filter(todo => todo.completed === false);
  render();
}
const filterCompletedCheck = () => {
  todos = todos.filter(todo => todo.completed === true);
  render();
}
const deleteTodo = ({id}) => {
  todos= todos.filter(todo => todo.id !== +id );
  updateData()
}


window.addEventListener('DOMContentLoaded', () =>{
  todos = fetchTodos();
  sortTodo();
  data = [...todos];
  console.log(data);
  render();
})


$input.onkeyup = e => {
  if( e.key !=='Enter' || $input.value ==='') return;
  addTodo(e.target.value);
  $input.value ='';
  render();
}

$todos.onchange = e =>{
  if(!e.target.matches('li > input')) return;
  const $checkParent = e.target.parentNode;
  todosCheck($checkParent);
  updateData();
  const $curFilter = document.querySelector('.nav .active');
  if($curFilter.matches('#active')){
    filterActiveCheck();
  }
  if($curFilter.matches('#completed')){
    filterCompletedCheck();
  }
  render();
}
$todos.onclick = e => {
  if(!e.target.matches('.remove-todo')) return;
  const $buttonParent = e.target.parentNode;
  deleteTodo($buttonParent);
  $todos.removeChild($buttonParent);
}

$filter.onclick = e => {
  if(!e.target.matches('li')) return;
  [...$filter.children].forEach(item => {
    item.classList.toggle('active',e.target === item);
  })
  // let data = todos;
  if(e.target.matches('#all')){
    todos = data;
    render();
    updateData()
  }

  if(e.target.matches('#active')){
    todos = data.filter(todo => {
      return todo.completed === false;
    });

    render();
    updateData()
    // todos = data;
  }
  if(e.target.matches('#completed')){
    todos = data.filter(todo => {
      return todo.completed ===true;
    })

    render();
    updateData()
    // todos = data;
  }
}

$clear.onclick = e => {
  if(!e.target.matches('.btn')) return;
  todos = todos.map(todo => {
    return {...todo, ...{completed : false}};
  })

  render();
  updateData();
}
$completeAll.onchange = e => {
  if(e.target.checked){
    todos= todos.map(todo => {
    return{...todo, ...{completed : true}};
    })
    updateData()
  }
  if(!e.target.checked){
    todos= todos.map(todo => {
    return{...todo, ...{completed : false}};
    })
    updateData()
  }
  const $curFilter = document.querySelector('.nav .active');
  if($curFilter.matches('#active')){
    filterActiveCheck();
  }
  if($curFilter.matches('#completed')){
    filterCompletedCheck();
  }
  render();
}
```
