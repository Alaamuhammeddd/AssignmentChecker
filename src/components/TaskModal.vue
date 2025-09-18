<script setup>
import { ref } from "vue";
const emit = defineEmits(["close-modal", "add-task"]);
const taskName = ref("");

const handleClose = () => {
  emit("close-modal");
};

const handleSubmit = (e) => {
  e.preventDefault();
  if (taskName.value.trim()) {
    emit("add-task", {
      id: Date.now(),
      name: taskName.value,
      status: "in-progress",
    });
    taskName.value = "";
    handleClose();
  }
};
</script>
<template>
  <div class="task-modal">
    <button @click="handleClose">X</button>
    <h2 class="task-modal__title">Add Task</h2>
    <form class="task-modal__form" @submit="handleSubmit">
      <div class="task-modal__form-group">
        <label class="task-modal__form-group-label">Task Name</label>
        <input
          v-model="taskName"
          class="task-modal__form-group-input"
          type="text"
        />
      </div>
      <button class="task-modal__button" type="submit">Add Task</button>
    </form>
  </div>
</template>
<style scoped lang="scss">
@use "../styles/__variables" as *;
.task-modal {
  background-color: $website-color;
  color: $white-text-color;
  padding: 20px;
  border-radius: 5px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1000;
  min-width: 300px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
.task-modal__title {
  font-size: 24px;
  font-weight: 600;
}
.task-modal__form {
  display: flex;
  flex-direction: column;
}
.task-modal__form-group {
  display: flex;
  flex-direction: column;
}
.task-modal__form-group-label {
  font-size: 16px;
  font-weight: 600;
}
.task-modal__form-group-input {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid $white-text-color;
}
.task-modal__button {
  padding: 10px;
  border-radius: 5px;
}
.task-modal__button:hover {
  background-color: $website-color-secondary;
  color: $white-text-color;
}
</style>
