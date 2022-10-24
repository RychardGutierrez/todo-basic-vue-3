<template>
  <section class="create-todo">
    <h3>CREATE A TODO</h3>
    <form @submit.prevent="addTodo">
      <h4>What's on your todo list?</h4>
      <input type="text" placeholder="e.g. make a todo" v-model="inputContent" />
      <h4>Pick a category</h4>
      <div class="options">
        <label>
          <input type="radio" name="category" value="business" v-model="inputCategory" />
          <span class="bubble business"></span>
          <div>Business</div>
        </label>
        <label>
          <input type="radio" name="category" value="personal" v-model="inputCategory" />
          <span class="bubble personal"></span>
          <div>Personal</div>
        </label>
      </div>
      <button type="submit">Add Todo</button>
    </form>
  </section>
</template>

<script setup>
import { ref, defineEmits } from "vue";
const inputContent = ref("");
const inputCategory = ref(null);
const emit = defineEmits(['saveTodo'])

const addTodo = () => {
  if (inputContent.value.trim() === "" || inputCategory.value === null) {
    return alert("Ups incomplete data");
  }

  const todo = {
    content: inputContent.value,
    category: inputCategory.value,
    isDone: false,
    createdAt: new Date().getTime()
  }

  emit("saveTodo", todo);

  inputCategory.value = null;
  inputContent.value = "";
}

</script>

<style scoped>

</style>