<template>
    <div class="container">
        <TodoForm :todos="todos" />
        <TodoList :todos="todos" @edit-todo="" @remove-todo="removeTodo" @complete-todo="completeTodo" @deleteHandler="deleteHandler" />
    </div>
</template>

<script setup>
import '../style.css'
import TodoForm from './TodoForm.vue';
import TodoList from './TodoList.vue';
import { ref, provide, reactive } from 'vue';

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


const completeTodo = (id) => {
    const index = todos.value.findIndex((todo) => todo.id === id);
    const selectedTodo = { ...todos.value[index] };

    selectedTodo.isCompleted = !selectedTodo.isCompleted;

    const updatedTodos = [...todos.value];
    updatedTodos[index] = selectedTodo;
    todos.value = updatedTodos; 
}

const removeTodo = (id) =>{
    const filteredTodos = todos.value.filter((todo) => todo.id !== id)
    todos.value = filteredTodos
}

provide('addTodoItem', addTodoItem)
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