<template>
    <div class="container">
      <TodoForm :todos="todos" :get-completed-task-count="getCompletedTaskCount" />
      <TodoList :todos="todos" @remove-todo="removeTodo" @complete-todo="completeTodo" @deleteHandler="deleteHandler" />
    </div>
  </template>
  
  <script setup>
  import '../style.css'
  import TodoForm from './TodoForm.vue';
  import TodoList from './TodoList.vue';
  import { ref, provide, computed, onMounted } from 'vue';
  
  const todos = ref([]);
  
  onMounted(() => {
    const storedTodos = localStorage.getItem('todos');
    if (storedTodos) {
      todos.value = JSON.parse(storedTodos);
    }
  });
  
  function addTodoItem(todo) {
    todos.value.push({
      id: generateUniqueId(),
      text: todo,
      isCompleted: false
    });
    localStorage.setItem('todos', JSON.stringify(todos.value));
    // localStorage.clear('todos')
  }
  
  function generateUniqueId() {
    return Math.floor(Math.random() * 10000);
  }
  
  const getCompletedTaskCount = computed(() => {
    return todos.value.filter(todo => todo.isCompleted).length;
  });
  
  const completeTodo = (id) => {
    const index = todos.value.findIndex((todo) => todo.id === id);
    const selectedTodo = { ...todos.value[index] };
    selectedTodo.isCompleted = !selectedTodo.isCompleted;
    const updatedTodos = [...todos.value];
    updatedTodos[index] = selectedTodo;
    todos.value = updatedTodos;
    localStorage.setItem('todos', JSON.stringify(todos.value));
  }
  
  const removeTodo = (id) => {
    const filteredTodos = todos.value.filter((todo) => todo.id !== id);
    todos.value = filteredTodos;
    localStorage.setItem('todos', JSON.stringify(todos.value));
  }
  
  provide('addTodoItem', addTodoItem);
  </script>
  
  <style scoped>
  .container {
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 40rem;
    height: 100%;
    background-color: #fff;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin: 0 auto;
    padding: 19px;
  }
  </style>
  