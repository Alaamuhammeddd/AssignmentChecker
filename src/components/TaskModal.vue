<template>
  <div class="task-modal">
    <h2 class="task-modal__title">Add Task</h2>
    <form class="task-modal__form">
      <div class="task-modal__form-group">
        <label class="task-modal__form-group-label">Task Name</label>
        <input class="task-modal__form-group-input" type="text" />
      </div>
    </form>
    <button class="task-modal__button">Add Task</button>
    <button class="task-modal__button">Cancel</button>
  </div>
</template>
<style scoped lang="scss">
@use "../styles/__variables" as *;
.task-modal {
  background-color: $website-color;
  color: $white-text-color;
  padding: 20px;
  border-radius: 5px;
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
