<script setup>
const props = defineProps(["tarefas"]);
</script>

<template>
  <p class="mt-4" v-if="tarefas.length < 1">
    Você ainda não possui nenhuma tarefa cadastrada.
  </p>
  <ul class="list-group mt-4" v-else>
    <li class="list-group-item" v-for="tarefa in props.tarefas">
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
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
