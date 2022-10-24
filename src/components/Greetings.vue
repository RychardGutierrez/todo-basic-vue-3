<template>
  <section class="greeting">
    <h2 class="title">
      What's ups <input type="text" placeholder="Name here" v-model="name" />
    </h2>
  </section>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";
import { LOCAL_STORAGE_NAME } from "../common/constants";

const name = ref("");

watch(name, (value) => {
  localStorage.setItem(LOCAL_STORAGE_NAME, value);
})

onMounted(() => {
  name.value = localStorage.getItem(LOCAL_STORAGE_NAME);
})
</script>

<style scoped>

</style>