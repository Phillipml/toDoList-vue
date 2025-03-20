<script setup>
import { reactive } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import TasksList from "./components/TasksList.vue";

const allTasks = reactive({
  filter: "todas",
  tempTask: "",
  tasks: [
    {
      title: "Estudar ES6",
      completed: false,
    },
    {
      title: "Estudar SASS",
      completed: false,
    },
    {
      title: "Estudar VUE",
      completed: true,
    },
  ],
});
const getPendingTasks = () => {
  return allTasks.tasks.filter((tasks) => !tasks.completed);
};
const getCompletedTasks = () => {
  return allTasks.tasks.filter((tasks) => tasks.completed);
};
const getFilteredTasks = () => {
  const { filter } = allTasks;
  switch (filter) {
    case "pendentes":
      return getPendingTasks();
    case "finalizadas":
      return getCompletedTasks();
    default:
      return allTasks.tasks;
  }
};
const newTask = () => {
  const newTask = {
    title: allTasks.tempTask,
    completed: false,
  };
  allTasks.tasks.push(newTask);
  allTasks.tempTask = "";
};
</script>

<template>
  <div class="container">
    <Header :pendingTasks="getPendingTasks().length" />
    <Form
      :tempTask="allTasks.tempTask"
      :newTask="newTask"
      :changeTempTask="(event) => (allTasks.tempTask = event.target.value)"
      :changeFilter="(event) => (allTasks.filter = event.target.value)"
    />

    <TasksList :getFilteredTasks="getFilteredTasks()" />
  </div>
</template>
