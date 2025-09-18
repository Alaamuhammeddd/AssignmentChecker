<style scoped lang="scss">
@use "../styles/__variables" as *;
.assignment-header__button {
  background: $button-color;
  border: 2px solid $black-text-color;
  color: $black-text-color;
  font-weight: 600;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;

  &:hover {
    background: $button-color-hover;
    border: 2px solid $button-color-hover;
  }
}
</style>
<template>
  <div class="addTask">
    <button class="assignment-header__button" @click="openModal">
      Add Task
    </button>
    <TaskModal v-if="isModalOpen" />
  </div>
</template>
<script setup>
import { ref } from "vue";
import TaskModal from "./TaskModal.vue";
const isModalOpen = ref(false);
const openModal = () => {
  isModalOpen.value = true;
  console.log(isModalOpen.value);
};
</script>
