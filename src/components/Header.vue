<template>
  <section class="assignment-header">
    <div class="assignment-header__brand">
      <img
        src="../assets/logo.png"
        alt="Assignment Checker"
        class="assignment-header__logo"
      />
      <h1 class="assignment-header__title">Assignment Checker</h1>
    </div>
    <AddButton
      :inProgressTasks="inProgressTasks"
      @update:inProgressTasks="$emit('update:inProgressTasks', $event)"
    />
  </section>
</template>
<script setup>
import AddButton from "./AddButton.vue";

defineProps({
  inProgressTasks: {
    type: Array,
    required: true,
  },
});

defineEmits(["update:inProgressTasks"]);
</script>
<style scoped lang="scss">
@use "../styles/__variables" as *;
.assignment-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 3px solid $website-color-secondary;

  &__brand {
    display: flex;
    align-items: center;
  }

  &__logo {
    width: 50px;
    height: 50px;
    padding-inline-end: 10px;
  }
  &__title {
    font-size: 24px;
    font-weight: 600;
  }
}
</style>
