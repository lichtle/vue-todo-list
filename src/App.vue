<script setup>
import { reactive } from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue";
import ListaDeTarefas from "./components/ListaDeTarefas.vue";

const estado = reactive({
  filtro: "todas",
  tarefaASerCadastrada: "",
  tarefas: [],
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

  estado.tarefaASerCadastrada = ""; // Limpando o campo após a inserção da tarefa
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefasPendentes="getTarefasPendentes().length" />
    <Formulario
      :tarefa-a-ser-cadastrada="estado.tarefaASerCadastrada"
      :editar-tarefa-a-ser-cadastrada="
        (evento) => (estado.tarefaASerCadastrada = evento.target.value)
      "
      :cadastrar-tarefa="cadastrarTarefa"
      :filtro="(evento) => (estado.filtro = evento.target.value)"
    />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>


