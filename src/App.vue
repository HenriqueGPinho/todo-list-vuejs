<script setup>
  import { ref } from 'vue';

  const estado = ref({
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false
      },
      {
        titulo: 'Estudar Bootstrap',
        finalizada: false
      }
    ]
  });
</script>

<template>
  <div class="container">
    <header class="p-5 mt-4 mb-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui 7 tarefas pendentes</p>
    </header>

    <form>
      <div class="row">
        <div class="col-md-6">
          <input class="form-control" type="text" placeholder="O que você precisa fazer?">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Salvar</button>
        </div>
        <div class="col-md-4">
          <select class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Taferas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in estado.tarefas">
        <input :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
