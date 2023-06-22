<template>
    <section>
        <article class="todo" v-for="(todo, index) in props.todos" :key="index">
            <h3>{{ todo.text }}</h3>
            <article>
                <button>Edit</button>
                <button @click="() => emit('complete-todo', todo.id)">
                    Complete
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
const emit = defineEmits(['complete-todo']);


</script>

<style scoped>
.todo {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 20rem;
    margin: 10px 0;
}
</style>