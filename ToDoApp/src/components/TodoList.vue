<template>
    <section>
        <article :class="todo.isCompleted ? 'completed todo' : 'todo'" v-for="(todo, index) in props.todos" :key="index">
            <h3 @click="() => emit('complete-todo', todo.id)">{{ todo.text }}</h3>
            <article class="btns">
                <button class="editBtn" @click="() => emit('edit-todo', todo)">
                    Edit
                </button>
                <button class="removeBtn" @click="() => emit('remove-todo', todo.id)">
                    Delete
                </button>
            </article>
        </article>
    </section>
</template>

<script setup>
import { ref, defineProps, defineEmits,onMounted } from 'vue';
const props = defineProps({
  todos: Array
});

const emit = defineEmits(['complete-todo', 'remove-todo', 'edit-todo']);

</script>

<style scoped>
.todo {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 20rem;
    margin: 10px 0;
    border: 1px solid #9BA4B5;
    border-radius: 5px;
    width: 23rem;
    height: 3rem;
    padding: 1rem;
}

.todo h3 {
    cursor: pointer;
}

.completed {
    text-decoration: line-through;
    color: #394867
}

.removeBtn {
    color: crimson;
    background-color: #fff;
    border: 1px solid crimson;
    border-radius: 5px;
    outline: none;
    padding: 5px 10px;
    cursor: pointer;
}

.removeBtn:hover {
    color: white;
    background-color: crimson;
}
.editBtn{
    margin-right: 10px;
    color: #394867;
    background-color: #fff;
    border: 1px solid #394867;
    border-radius: 5px;
    outline: none;
    padding: 5px 10px;
    cursor: pointer;
}
.editBtn:hover{
    color: white;
    background-color: #394867;
    font-size: 14px;
}
</style>