<script setup>
import { reactive } from "vue";

const state = reactive({
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
  return state.tasks.filter((tasks) => !tasks.completed);
};
const getCompletedTasks = () => {
  return state.tasks.filter((tasks) => tasks.completed);
};
const getFilteredTasks = () => {
  const { filter } = state;
  switch (filter) {
    case "pendentes":
      return getPendingTasks();
    case "finalizadas":
      return getCompletedTasks();
    default:
      return state.tasks;
  }
};
const cadastraTarefa = () => {
  const newTask = {
    title: state.tempTask,
    completed: false,
  };
  state.tasks.push(newTask);
  state.tempTask = "";
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui {{ getPendingTasks().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input
            :value="state.tempTask"
            @change="(event) => (state.tempTask = event.target.value)"
            required
            type="text"
            placeholder="Digite aqui a descrição da tarefa"
            class="form-control"
          />
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select
            class="form-control"
            @change="(event) => (state.filter = event.target.value)"
          >
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4" v-for="tasks in getFilteredTasks()">
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
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
