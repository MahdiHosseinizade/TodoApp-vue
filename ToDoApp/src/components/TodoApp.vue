<template>
    <div class="container">
        <h2>this is test</h2>
        <TodoForm />
        <TodoList />
    </div>
</template>

<script setup>
import '../style.css'
import TodoForm from './TodoForm.vue';
import TodoList from './TodoList.vue';
</script>

<style scoped>
.container {
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 40rem;
    /* height: 40vh; */
    background-color: #fff;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 4px;
}
</style>