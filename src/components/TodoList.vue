<template>
  <section class="todo-list">
    <h3>TODO LIST</h3>
    <div class="list">
      <div v-for="todo in todos" :class="`todo-item ${todo.done && 'done'} `" :key="todo.createdAt">
        <label>
          <input type="checkbox" v-model="todo.done" />
          <span :class="`bubble ${todo.category}`"></span>
        </label>
        <div class="todo-content">
          <input type="text" v-model="todo.content" />
        </div>
        <div class="actions">
          <button class="delete" @click="deleteTodo(todo)">Delete</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { defineEmits } from "vue";
const emit = defineEmits(['deleteTodo'])
const props = defineProps({
  todos: {
    type: Array,
    requited: true
  }
})

const deleteTodo = (todo) => {
  emit("deleteTodo", todo)
}

</script>

<style scoped>

</style>