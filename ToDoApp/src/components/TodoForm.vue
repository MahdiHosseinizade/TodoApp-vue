<template>
  <form class="formControl" @submit="submitHandler">
    <input placeholder="Add Todo..." type="text" v-model="todo" />
    <button class="addBtn" type="submit">Add</button>
  </form>
  <h3 class="show-completed-task" v-if="todos.length > 0">
    <span class="task-count">{{ getCompletedTaskCount }}</span> {{ getCompletedTaskCount <= 1 ? 'task' : 'tasks' }} completed
  </h3>
  <h3 class="show-completed-task" v-else>
    Add some todo
  </h3>
</template>

<script setup>
import { ref, defineProps, computed, onMounted } from 'vue';

const todo = ref('');
const props = defineProps({
  todos: Array,
  getCompletedTaskCount: Function,
  addTodoItem:Function
});


function submitHandler(e) {
  e.preventDefault();
  const trimmedTodo = todo.value.trim();
  if (trimmedTodo === '') {
    alert('Please enter a todo');
  }
  else if (trimmedTodo !== '') {
    props.addTodoItem(trimmedTodo);
    todo.value = '';
  }
}


const getCompletedTaskCount = computed(() => {
  return props.todos.filter(todo => todo.isCompleted).length;
});
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
  color: #394867;
    background-color: #fff;
    border: 1px solid #394867;
    border-radius: 5px;
    outline: none;
    padding: 5px 15px;
    cursor: pointer;
    font-size: 15px;
}
.addBtn:hover{
  background-color: #394867;
  color: white;
}
.task-count{
  width: 20px;
  height: 20px;
  background-color: #394867;
  border-radius: 50%;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 5px;
}
.show-completed-task{
  display: flex;
  flex-direction: row;

}
</style>