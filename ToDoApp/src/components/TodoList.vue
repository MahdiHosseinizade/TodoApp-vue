<template>
    <section >
        <article :class="todo.isCompleted ? 'completed todo' : 'todo'" v-for="(todo, index) in props.todos" :key="index">
            <h3 @click="() => emit('complete-todo', todo.id)">{{ todo.text }}</h3>
            <article>
                <button class="removeBtn" @click="() => emit('remove-todo' ,todo.id)" >
                    Delete
                </button>
            </article>
        </article>
    </section>
</template>

<script setup>
import { ref, defineProps,defineEmits } from 'vue';
const props = defineProps({
    todos: Array
})
const emit = defineEmits(['complete-todo','remove-todo']);


</script>

<style scoped>
.todo {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 20rem;
    margin: 10px 0;
}
.todo h3{
    cursor: pointer;
}
.completed{
    text-decoration: line-through;
    color: #804040;
}
.removeBtn{
    color: crimson;
    background-color: #fff;
    border: 1px solid crimson;
    border-radius: 5px;
    outline: none;
    padding: 5px 10px;
    cursor: pointer;
}
.removeBtn:hover{
    color: white;
    background-color: crimson;
}
</style>