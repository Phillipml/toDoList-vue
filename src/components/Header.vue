<script setup>
const props = defineProps(["pendingTasks"]);
</script>

<template>
  <header>
    <h1>Minhas Tarefas</h1>
    <p>Você possui {{ pendingTasks }} tarefas pendentes</p>
  </header>
</template>
