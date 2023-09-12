<template>
  <div class="todo-item">
    <el-checkbox
      v-model="todo.isDone"
      @change="onChange"
      size="large"
      :label="todo.name"
      :class="todo.isDone ? 'done' : ''"
    />
    <el-tag @click="$emit('delete')" type="danger">delete</el-tag>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
const emit = defineEmits(['check', 'delete']);

defineProps({
  todo: Object
});

onMounted(() => {});

const onChange = (val) => {
  // emit('check', val);
};
</script>

<style lang="scss" scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 8px;
  margin-bottom: 8px;
  border: 1px solid lightgray;
  border-radius: 6px;
  text-align: center;
  &:hover {
    .el-tag {
      visibility: visible;
    }
  }
  :deep(.el-checkbox) {
    .el-checkbox__label {
      font-size: 16px;
      font-weight: bold;
      transform: translateY(-2px);
    }
    &.done {
      .el-checkbox__label {
        text-decoration: line-through;
      }
    }
  }
  .el-tag {
    visibility: hidden;
    cursor: pointer;
  }
}
</style>
