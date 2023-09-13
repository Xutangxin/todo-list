<template>
  <div class="todo-item">
    <el-checkbox
      v-model="todo.isDone"
      @change="$emit('check')"
      size="large"
      :label="todo.name"
      :class="todo.isDone ? 'done' : ''"
    />
    <el-button @click="$emit('delete')" type="danger" icon="Delete"></el-button>
  </div>
</template>

<script setup>
defineProps({
  todo: Object
});
defineEmits(['check', 'delete']);
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
    .el-button {
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
  .el-button {
    padding: 8px;
    visibility: hidden;
    cursor: pointer;
  }
}
</style>
