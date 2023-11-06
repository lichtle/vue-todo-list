<script setup>
import { reactive } from "vue";

const estado = reactive({
  filtro: "todas",
  tarefaASerCadastrada: "",
  tarefas: [
    {
      titulo: "Estudar ES6",
      finalizada: false,
    },
    {
      titulo: "Estudar Sass",
      finalizada: false,
    },
    {
      titulo: "Ir para a academia",
      finalizada: true,
    },
  ],
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada === false);
};

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada);
};

const getTarefasFiltradas = () => {
  const filtro = estado.filtro;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
};

const cadastrarTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaASerCadastrada,
    finalizada: false,
  };

  estado.tarefas.push(novaTarefa);

  estado.tarefaASerCadastrada = "" // Limpando o campo após a inserção da tarefa
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <!-- A função preventDefault() pode ser substituída por um simples "prevent" após o nome do evento (submit) -->
      <div class="row">
        <div class="col">
          <input
            type="text"
            required
            :value="estado.tarefaASerCadastrada"
            @change="
              (evento) => (estado.tarefaASerCadastrada = evento.target.value)
            "
            class="form-control"
            placeholder="Escreva uma nova tarefa"
          />
        </div>
        <div class="col-md-1">
          <button type="submit" class="btn btn-primary">Adicionar</button>
        </div>
        <div class="col-md-2">
          <select
            class="form-control"
            @change="(evento) => (estado.filtro = evento.target.value)"
          >
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas concluídas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input
          type="checkbox"
          @change="(evento) => (tarefa.finalizada = evento.target.checked)"
          :checked="tarefa.finalizada"
          :id="tarefa.titulo"
        /><label
          :for="tarefa.titulo"
          class="ms-2"
          :class="{ done: tarefa.finalizada === true }"
          >{{ tarefa.titulo }}</label
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
