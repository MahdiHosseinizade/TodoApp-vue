<template>
  <div class="container">
    <TodoForm :todos="todos" :get-completed-task-count="getCompletedTaskCount" />
    <template v-if="!isEditingTodo">
      <TodoList :todos="todos" @edit-todo="EditHandler" @remove-todo="removeTodo" @complete-todo="completeTodo" @deleteHandler="deleteHandler" />
    </template>
    <template v-else>
      <EditTodo :todo="editingTodo" @update-todo="updateTodo" />
    </template>
  </div>
</template>
  
<script setup>
import '../style.css'
import EditTodo from './EditTodo.vue';
import TodoForm from './TodoForm.vue';
import TodoList from './TodoList.vue';
import { ref, provide, computed, onMounted } from 'vue';

const todos = ref([]);
const editingTodo = ref(null);

function EditHandler(todo) {
  editingTodo.value = todo;
}
const isEditingTodo = computed(() => {
  return editingTodo.value !== null;
})

function updateTodo(newTodo, id) {
  const index = todos.value.findIndex(todo => todo.id === id);
  if (index !== -1) {
    todos.value[index].text = newTodo;
    localStorage.setItem('todosItem', JSON.stringify(todos.value));
  }
  editingTodo.value = null;
}
onMounted(() => {
  const storedTodos = localStorage.getItem('todosItem');
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
  
  localStorage.setItem('todosItem', JSON.stringify(todos.value));

  // localStorage.clear('todos')
}

function generateUniqueId() {
  return Math.floor(Math.random() * 10000);
}

const getCompletedTaskCount = computed(() => {
  return todos.value.filter(todo => todo.isCompleted).length;
});

// const EditHandler = (todo) =>{
//   console.log(todo);
// }

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
  