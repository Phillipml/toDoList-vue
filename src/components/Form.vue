<script setup>
const props = defineProps([
  "newTask",
  "tempTask",
  "changeFilter",
  "changeTempTask",
]);
</script>
<template>
  <form @submit.prevent="newTask">
    <div class="row">
      <div class="col">
        <input
          :value="tempTask"
          @change="changeTempTask"
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
        <select class="form-control" @change="changeFilter">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
