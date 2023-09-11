<template>
  <div class="todo-input">
    <el-input
      v-model="inputVal"
      placeholder="please input"
      @keypress.enter="submit"
    />
    <el-button type="primary" @click="submit" :disabled="!inputVal"
      >submit</el-button
    >
  </div>
</template>

<script setup>
import { ref } from 'vue';
const emit = defineEmits(['submit']);
const inputVal = ref('');

const submit = () => {
  if (!inputVal.value) return;
  emit('submit', inputVal.value);
  inputVal.value = '';
};
</script>

<style lang="scss" scoped>
.todo-input {
  display: flex;
  font-size: 16px;
  margin-bottom: 16px;
  .el-input {
    width: 300px;
    margin-right: 8px;
    ::v-deep .el-input__inner {
      height: 42px;
    }
  }
  .el-button {
    height: 42px;
  }
}
</style>
