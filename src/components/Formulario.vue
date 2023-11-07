<script setup>
const props = defineProps([
  "cadastrarTarefa",
  "tarefaASerCadastrada",
  "filtro",
  "editarTarefaASerCadastrada",
]);
</script>

<template>
  <form @submit.prevent="props.cadastrarTarefa">
    <!-- A função preventDefault() pode ser substituída por um simples "prevent" após o nome do evento (submit) -->
    <div class="row">
      <div class="col">
        <input
          type="text"
          required
          :value="props.tarefaASerCadastrada"
          @change="props.editarTarefaASerCadastrada"
          class="form-control"
          placeholder="Escreva uma nova tarefa"
        />
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary">Adicionar</button>
      </div>
      <div class="col-md-2">
        <select class="form-control" @change="props.filtro">
          <option value="todas">Todas as tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas concluídas</option>
        </select>
      </div>
    </div>
  </form>
</template>
