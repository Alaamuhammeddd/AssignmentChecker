<script setup>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { faTrash, faCheck } from "@fortawesome/free-solid-svg-icons";

defineProps({
  inProgressTasks: {
    type: Array,
    default: () => [],
  },
  finishedTasks: {
    type: Array,
    default: () => [],
  },
});

const emit = defineEmits(["deleteTask", "completeTask"]);
</script>
<template>
  <div class="listed-assignments">
    <section class="listed-assignments__inProgress">
      <h2 class="listed-assignments__inProgress-title">In Progress...</h2>
      <div class="listed-assignments__inProgress-list">
        <div v-for="task in inProgressTasks" :key="task.id" class="task-item">
          <span>{{ task.name }}</span>
          <div class="listed-assignments__inProgress-actions">
            <button
              class="task-item__check"
              @click="emit('completeTask', task.id)"
            >
              <span class="task-item__check-icon">
                <FontAwesomeIcon :icon="faCheck" />
              </span>
            </button>
            <button
              class="task-item__delete"
              @click="emit('deleteTask', task.id)"
            >
              <span class="task-item__delete-icon"
                ><FontAwesomeIcon :icon="faTrash" />
              </span>
            </button>
          </div>
        </div>
      </div>
    </section>
    <section class="listed-assignments__finished">
      <h2 class="listed-assignments__finished-title">Finished</h2>
      <div class="listed-assignments__finished-list">
        <div
          v-for="task in finishedTasks"
          :key="task.id"
          class="task-item task-item--completed"
        >
          <span>{{ task.name }}</span>
          <button
            class="task-item__delete"
            @click="emit('deleteTask', task.id)"
          >
            <span class="task-item__delete-icon">
              <FontAwesomeIcon :icon="faTrash" />
            </span>
          </button>
        </div>
      </div>
    </section>
  </div>
</template>
<style lang="scss" scoped>
@use "../styles/__variables" as *;
.listed-assignments {
  display: flex;
  flex-direction: column;
  gap: 20px;
  height: 100%;
  padding: 20px;
  &__inProgress {
    padding: 20px;
    border-radius: 5px;
    &-title {
      color: #ff8888;
      font-size: 20px;
      font-weight: 600;
      margin-bottom: 10px;
    }
    &-actions {
      display: flex;
      gap: 10px;
    }
    &-list {
      display: flex;
      flex-direction: column;
      gap: 10px;

      .task-item {
        background-color: #ff888895;
        padding: 10px;
        border-radius: 5px;
        font-size: 16px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        &__check-icon {
          background: transparent;
          border: none !important;
          color: #000000dc;
          font-size: 20px;
          cursor: pointer;
          padding: 0 5px;
          display: flex;
          align-items: center;
          justify-content: center;
        }
        &__delete,
        &__check {
          background: none;
          border: none;
          color: #000000dc;
          font-size: 20px;
          cursor: pointer;
          padding: 0 5px;
          display: flex;
          align-items: center;
          justify-content: center;
          border-radius: 3px;

          &:hover {
            background-color: rgba(255, 68, 68, 0.1);
          }

          &-icon {
            line-height: 1;
          }
        }
      }
    }
  }
  &__finished {
    padding: 20px;
    border-radius: 5px;
    &-title {
      color: #88ffbc;
      font-size: 20px;
      font-weight: 600;
      margin-bottom: 10px;
    }
    &-list {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
  }
}
</style>
