<template>
  <div class="todo-filter">
    <el-tag
      v-for="(item, index) in statusOptions"
      :key="index"
      @click="onClick(item)"
      size="large"
      :effect="item === status ? 'light' : 'plain'"
      >{{ item }}</el-tag
    >
  </div>
</template>

<script setup>
import { ref } from 'vue';
const emit = defineEmits(['change']);
const status = ref('all');
const statusOptions = ref(['all', 'todo', 'done']);
const onClick = (val) => {
  emit('change', val);
  status.value = val;
};
</script>

<style lang="scss" scoped>
.todo-filter {
  display: flex;
  margin-bottom: 16px;
  .el-tag {
    margin-right: 16px;
    padding: 0 12px;
    cursor: pointer;
    :deep(.el-tag__content) {
      font-size: 14px;
    }
  }
}
</style>
