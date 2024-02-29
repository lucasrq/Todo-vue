<script setup>
import { reactive } from 'vue';
import Cabeca from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaTarefas from './components/ListaTarefas.vue';

const estado = reactive({
  filtro: "todas",
  tarefaTemporari: '',
  tarefas: [
    {
      titulo: 'estudar ES6',
      finalizada: false
    },
    {
      titulo: 'estudar SASS',
      finalizada: false
    },
    {
      titulo: 'estudar TypeScript',
      finalizada: false
    },
    {
      titulo: 'estudar React',
      finalizada: false
    },
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}
const getTarefasFiltradas = () => {
  const { filtro } = estado

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
    titulo: estado.tarefaTemporari,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaTemporari = ''
}



</script>

<template>
  <div class="container">
    <Cabeca :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocarFiltro="evento => estado.filtro = evento.target.value" :tarefaTemporari="estado.tarefaTemporari"
      :editaTarefaTemp="evento => estado.tarefaTemporari = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
