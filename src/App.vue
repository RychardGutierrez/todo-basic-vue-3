<script setup>
import { ref, onMounted, computed, watch } from "vue";
import CreateTodo from "./components/CreateTodo.vue";
import Greetings from "./components/Greetings.vue";
import TodoList from "./components/TodoList.vue";

import { LOCAL_STORAGE_TODOS } from "./common/constants";

const todos = ref([]);

const todosAsc = computed(() =>
  todos.value.sort((todoA, todoB) => todoB.createdAt - todoA.createdAt)
)

watch(todos, updatedTodos => {
  localStorage.setItem(LOCAL_STORAGE_TODOS, JSON.stringify(updatedTodos));
}, { deep: true })

onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem(LOCAL_STORAGE_TODOS) || []);
})

const saveTodo = (todo) => {
  todos.value.push(todo);
}

const deleteTodo = (data) => {
  todos.value = todos.value.filter((todo) => todo.createdAt !== data.createdAt);
}
</script>

<template>
  <main class="app">
    <div class="container">
      <Greetings />
      <CreateTodo @save-todo="saveTodo" />
      <TodoList :todos="todosAsc" @delete-todo="deleteTodo" />
    </div>
  </main>
</template>

<style scoped>

</style>
