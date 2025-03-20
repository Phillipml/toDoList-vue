<script setup>
const props = defineProps(["getFilteredTasks"]);
</script>
<template>
  <ul class="list-group mt-4" v-for="tasks in getFilteredTasks">
    <li class="list-group-item">
      <input
        @change="(event) => (tasks.completed = event.target.checked)"
        :checked="tasks.completed"
        :id="tasks.title"
        type="checkbox"
      />
      <label
        :for="tasks.title"
        :class="{ done: tasks.completed }"
        class="ms3"
        >{{ tasks.title }}</label
      >
    </li>
  </ul>
</template>
<style scoped>
.done {
  text-decoration: line-through;
}
</style>
