<script setup>
  import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false
      },
      {
        titulo: 'Estudar Bootstrap',
        finalizada: true
      },
      {
        titulo: 'Ler documentação do VueJS',
        finalizada: false
      }
    ]
  });

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada);
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada);
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
      const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mt-4 mb-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>

    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col-md-6">
          <input :value="estado.tarefaTemp" @change="e => estado.tarefaTemp = e.target.value" required class="form-control" type="text" placeholder="O que você precisa fazer?">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Salvar</button>
        </div>
        <div class="col-md-4">
          <select class="form-control" @change="e => estado.filtro = e.target.value">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Taferas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
