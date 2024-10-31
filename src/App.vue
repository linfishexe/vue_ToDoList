<style>
* {
  position: relative;
}

body {
  display: block;
}

#app {
  width: 500px;
  height: auto;
  top: 60px;
}

.title {
  text-align: center;
  margin: 0 0 10px 0;
}

#form {
  display: flex;
}

#form div input {
  width: 400px;
  margin: 10px 5px;
  padding: 10px;
  outline: none;
  border: 2px solid #ccc;
  border-radius: 5px;
  flex-grow: 1;
}

#form div button {
  margin: 10px;
  width: 60px;
  height: 40px;
  border: none;
  border-radius: 5px;
  background: #63b185;
}
ul {
  padding: 0;
  width: 100%;
}

ul li div {
  width: 100%;
  border: 0;
  border-bottom: 2px solid #ccc;
  margin-bottom: 10px;
}
ul li div p {
  width: 80%;
  font-size: 15x;
  padding: 0 20px;
  top: 50%;
  transform: translateY(-50%);
  text-overflow: ellipsis;
}

ul li input {
  margin: 10px 5px;
  width: 10%;
  height: 30px;
  border: none;
  border-radius: 5px;
}

ul li button {
  margin: 10px 5px;
  width: 10%;
  border: none;
  border-radius: 5px;
}

.done {
  background: #6cb9c2;
}
.delete {
  background: #c12424;
}

.todo_done_text {
  text-decoration: line-through;
}
</style>
<script setup>
import AddTodo from './components/AddTodo.vue'
import TodoList from './components/TodoList.vue'
import { ref } from 'vue'

const todos = ref([
  {
    id: 1,
    text: 'text',
  },
])

const handleAddTodo = todo => {
  todos.value.push(todo)
}

const handleDeleteTodo = todoID => {
  // filter: 判斷並留下符合條件的ID，不符合的被過濾掉
  todos.value = todos.value.filter(todo => todo.id !== todoID)
}

const handleCompleteTodo = todoID => {
  todos.value = todos.value.map(todo =>
    todo.id === todoID ? { ...todo, complete: !todo.complete } : todo,
  )
}

const handleEditTodo = todoID => {
  todos.value = todos.value.map(todo =>
    todo.id === todoID ? { ...todo, editing: !todo.editing } : todo,
  )
}
</script>

<template>
  <div>
    <AddTodo @Add-todo="handleAddTodo" />
    <TodoList
      :todos="todos"
      @deleteTodo="handleDeleteTodo"
      @completeTodo="handleCompleteTodo"
      @editTodo="handleEditTodo"
    />
  </div>
</template>
