<template>
    <form @submit="submitHandler">
      <input type="text" v-model="todo" />
      <button  type="submit">Add</button>
    </form>
  </template>
  
  <script setup>
  import { ref,defineProps ,inject} from 'vue';
  
  const todo = ref('');
  const props = defineProps({
    todos :Array
  })
  const addTodoItem = inject('addTodoItem');
  
  
  function submitHandler(e) {
    e.preventDefault();
    const trimmedTodo = todo.value.trim();
    if (trimmedTodo !== '') {
      addTodoItem(trimmedTodo);
      todo.value = '';
    }

  }
  

  </script>
  