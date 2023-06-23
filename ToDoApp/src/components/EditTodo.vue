<template>
  <h3>
    Update Todo
  </h3>
    <form class="formControl" @submit="submitHandler">
        <input placeholder="Update Todo..." type="text" v-model="newTodo" />
        <button class="addBtn" type="submit">Update</button>
    </form>
</template>

<script setup>
import { defineProps, defineEmits, ref } from 'vue'
const props = defineProps({
  todo: Object
});

const emit = defineEmits(['update-todo']);

const newTodo = ref(props.todo.text);

function submitHandler(e) {
  e.preventDefault();
  const trimmedTodo = newTodo.value.trim();
  if (trimmedTodo === '') {
    alert('Please enter a todo');
  }
  else {
    emit('update-todo', trimmedTodo, props.todo.id);
    newTodo.value = '';
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
  border: 2px solid #394867;
}
.formControl{
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 20rem;
  margin-top: 20px;
}
.addBtn{
  border: 1px solid #394867;
  border-radius: 5px;
  padding: 5px 10px;
  outline: none;
  cursor: pointer;
  background-color: #fff;
  color: #394867;
}
.addBtn:hover{
  background-color: #394867;
  color: white;
}

</style>