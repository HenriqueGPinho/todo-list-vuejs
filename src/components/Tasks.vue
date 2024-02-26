<script setup>
const props = defineProps(['tarefas']);
</script>

<template>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo"
        type="checkbox">
      <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
    </li>
  </ul>
  <p v-if="props.tarefas.length == 0" class="p-2 text-center bg-light rounded-3">Não há tarefas a exibir</p>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>