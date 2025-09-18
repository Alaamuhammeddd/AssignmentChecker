<script setup>
import { ref, onMounted, watch } from "vue";
import AssignmentsList from "./components/AssignmentsList.vue";
import Header from "./components/Header.vue";

// Load tasks from localStorage or default to empty array
const loadTasks = () => {
  try {
    const savedInProgress = localStorage.getItem("inProgressTasks");
    const savedFinished = localStorage.getItem("finishedTasks");

    return {
      inProgress: savedInProgress ? JSON.parse(savedInProgress) : [],
      finished: savedFinished ? JSON.parse(savedFinished) : [],
    };
  } catch (error) {
    console.error("Error loading tasks:", error);
    return { inProgress: [], finished: [] };
  }
};

// Initialize tasks with data from localStorage
const { inProgress, finished } = loadTasks();
const inProgressTasks = ref(inProgress);
const finishedTasks = ref(finished);
const handleCompleteTask = (taskId) => {
  const taskToComplete = inProgressTasks.value.find(
    (task) => task.id === taskId
  );
  if (taskToComplete) {
    inProgressTasks.value = inProgressTasks.value.filter(
      (task) => task.id !== taskId
    );
    finishedTasks.value.push({ ...taskToComplete, status: "completed" });
  }
};
// Save tasks to localStorage
const saveTasks = () => {
  localStorage.setItem(
    "inProgressTasks",
    JSON.stringify(inProgressTasks.value)
  );
  localStorage.setItem("finishedTasks", JSON.stringify(finishedTasks.value));
};

// Watch for changes in both task lists
watch(
  [inProgressTasks, finishedTasks],
  () => {
    saveTasks();
  },
  { deep: true, immediate: true }
);

const handleDeleteTask = (taskId) => {
  inProgressTasks.value = inProgressTasks.value.filter(
    (task) => task.id !== taskId
  );
  finishedTasks.value = finishedTasks.value.filter(
    (task) => task.id !== taskId
  );
};
</script>

<template>
  <div class="assignment-container">
    <Header
      :inProgressTasks="inProgressTasks"
      @update:inProgressTasks="inProgressTasks = $event"
    />
    <AssignmentsList
      :inProgressTasks="inProgressTasks"
      :finishedTasks="finishedTasks"
      @completeTask="handleCompleteTask"
      @deleteTask="handleDeleteTask"
    />
  </div>
</template>

<style scoped lang="scss">
.assignment-container {
  width: 100%;
  height: 100%;
}
</style>
