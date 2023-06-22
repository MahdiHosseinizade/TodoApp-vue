<template>
  <form class="formControl" @submit="submitHandler">
    <input type="text" v-model="todo" />
    <button class="addBtn" type="submit">Add</button>
  </form>
</template>
  
<script setup>
import { ref, defineProps, inject } from 'vue';

const todo = ref('');
const props = defineProps({
  todos: Array
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
 
<style scoped>
input{
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 5px 3px;
    outline: none;
    width: 200px;
}
input:focus{
  border: 2px solid cadetblue;
}
.formControl{
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 20rem;
  margin-bottom: 20px;
}
.button{
  color: aqua;
  background-color: #fff;
  border: 1px solid aqua;
  border-radius: 5px;
  outline: none;
  padding: 5px 10px;
  cursor: pointer;
}

.addBtn{
  color: rgb(190, 141, 19);
    background-color: #fff;
    border: 1px solid rgb(190, 141, 19);
    border-radius: 5px;
    outline: none;
    padding: 5px 10px;
    cursor: pointer;
}
.addBtn:hover{
  background-color: rgb(190, 141, 19);
  color: white;
}
</style>