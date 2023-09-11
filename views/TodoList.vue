<template>
  <div class="todo-list">
    <h1>Todo List</h1>
    <todo-input @submit="onSubmit"></todo-input>
    <div class="list">
      <todo-item
        v-for="(item, index) in list"
        :key="index"
        :todo="item"
        @check="onCheck(index, $event)"
        @delete="onDelete(index)"
      ></todo-item>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import TodoInput from './components/TodoInput.vue';
import TodoItem from './components/TodoItem.vue';
const list = ref([
  {
    name: 'this is an example',
    isDone: false
  }
]);

const onSubmit = (val) => {
  list.value.unshift({
    name: val,
    isDone: false
  });
};

const onCheck = (index, val) => {};
const onDelete = (index) => {
  list.value.splice(index, 1);
};
</script>

<style lang="scss" scoped>
.todo-list {
  height: 100%;
  padding: 16px;
  h1 {
    text-align: center;
    margin-bottom: 8px;
    font-weight: bold;
  }
  .list {
    max-height: calc(100vh - 220px);
    overflow: auto;
  }
}
</style>
