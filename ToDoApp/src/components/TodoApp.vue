<template>
    <div class="container">
        <h2>this is test</h2>
        <TodoForm :todos="todos" />
        <TodoList :todos="todos"/>
    </div>
</template>

<script setup>
import '../style.css'
import TodoForm from './TodoForm.vue';
import TodoList from './TodoList.vue';
import { ref, provide } from 'vue';

const todos = ref([]);
function addTodoItem(todo) {
  todos.value.push({
    id: generateUniqueId(),
    text: todo,
    isCompleted: false
  });
}

function generateUniqueId() {
  return Math.floor(Math.random() * 10000);
}
provide('addTodoItem',addTodoItem)
</script>

<style scoped>
.container {
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 40rem;
    height: 40vh;
    background-color: #fff;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin: 0 auto;
    padding: 19px;
}
</style>