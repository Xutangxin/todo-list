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
        @check="onCheck(index)"
      ></todo-item>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import TodoInput from './components/TodoInput.vue';
import TodoFilter from './components/TodoFilter.vue';
import TodoItem from './components/TodoItem.vue';

const list = ref([]);
const originList = ref([]);

const syncOriginList = () => {
  originList.value = JSON.parse(JSON.stringify(list.value));
};

const getHistory = () => {
  const todo = JSON.parse(localStorage.getItem('todo'));
  list.value = todo;
  syncOriginList();
};
getHistory();

const onSubmit = (val) => {
  const data = {
    name: val,
    isDone: false
  };
  list.value.unshift(data);
  syncOriginList();
};

const onDelete = (index) => {
  list.value.splice(index, 1);
  syncOriginList();
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

const onCheck = () => {
  syncOriginList();
};

watch(
  list.value,
  (val) => {
    localStorage.setItem('todo', JSON.stringify(val));
  },
  {
    deep: true,
    immediate: true
  }
);
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
