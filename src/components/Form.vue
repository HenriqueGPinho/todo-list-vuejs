<script setup>
  const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp']);
</script>

<template>
  <form @submit.prevent="props.cadastraTarefa">
      <div class="row">
        <div class="col-md-6 mt-2 mb-2">
          <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required class="form-control" type="text" placeholder="O que você precisa fazer?">
        </div>
        <div class="col-md-2 d-grid">
          <button class="btn btn-primary mt-2 mb-2" type="submit">Salvar</button>
        </div>
        <div class="col-md-4 mt-2 mb-2">
          <select class="form-select" @change="props.trocarFiltro">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Taferas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
</template>