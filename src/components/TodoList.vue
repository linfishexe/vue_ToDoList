<template>
  <ul v-if="todos.length > 0">
    <li v-for="todo in todos" :key="todo.id" style="display: flex">
      <input type="checkbox" @click="completeTodo(todo.id)" class="done" />

      <div>
        <p :class="{ todo_done_text: todo.complete }">
          {{ todo.text }}
        </p>
      </div>

      <button @click="deleteTodo(todo.id)" class="delete">x</button>
    </li>
  </ul>

  <p v-else>沒有代辦事項</p>
</template>

<script setup>
// text-decoration: line-through
import { defineProps, defineEmits } from 'vue'

defineProps({
  todos: {
    type: Array,
  },
})

const emit = defineEmits(['deleteTodo', 'completeTodo', 'editTodo'])

const deleteTodo = todoID => {
  emit('deleteTodo', todoID)
}

const completeTodo = todoID => {
  emit('completeTodo', todoID)
}
</script>
