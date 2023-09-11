<template>
  <main>
    <todo-list></todo-list>
  </main>
</template>

<script setup>
import TodoList from '../views/TodoList.vue';
</script>
<style scoped>
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>
