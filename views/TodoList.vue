<template>
  <div class="todo-list">
    <h1>Todo List</h1>
    <todo-input @submit="onSubmit"></todo-input>
    <todo-filter @change="onChange"></todo-filter>
    <div class="list">
      <todo-item
        v-for="(item, index) in list"
        :key="index"
        :todo="item"
        @delete="onDelete(index)"
      ></todo-item>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import TodoInput from './components/TodoInput.vue';
import TodoFilter from './components/TodoFilter.vue';
import TodoItem from './components/TodoItem.vue';
const list = ref([]);
const originList = ref([...list.value]);

const onSubmit = (val) => {
  const data = {
    name: val,
    isDone: false
  };
  list.value.unshift(data);
  originList.value.unshift(data);
};

const onDelete = (index) => {
  list.value.splice(index, 1);
  originList.value.splice(index, 1);
};

const onChange = (val) => {
  if (val === 'all') {
    list.value = JSON.parse(JSON.stringify(originList.value));
  } else if (val === 'todo') {
    list.value = originList.value.filter((i) => !i.isDone);
  } else if (val === 'done') {
    list.value = originList.value.filter((i) => i.isDone);
  }
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
