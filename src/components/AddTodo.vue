<template>
  <h1 class="title">To Do List</h1>
  <form id="form" @submit.prevent="onSubmit">
    <!--
            @是代表事件 ，
            @submit.prevent讓todo送出時不會做原本會做的事 ex.重整網頁 -->
    <div>
      <input type="text" placeholder="請輸入代辦事項" v-model="text" required />
    </div>
    <div>
      <button>新增</button>
    </div>
  </form>
</template>

<script setup>
import { ref, defineEmits } from 'vue'

const text = ref('')
const emit = defineEmits(['AddTodo'])
const onSubmit = () => {
  const todo = {
    id: crypto.randomUUID(), //UUID - 唯一識別
    text: text.value,
    complete: false,
  }
  emit('AddTodo', todo)
}
</script>
