<template>
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
  else if (trimmedTodo !== '') {
    emit('update-todo', trimmedTodo, props.todo.id);
    newTodo.value = '';
  }
}
</script>