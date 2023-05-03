<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue'
  import Formulario from './components/Formulario.vue'
  import ListaDeTarefas from './components/ListaDeTarefas.vue'

  const estado = reactive({
    tarefaTemp: '',
    filtro: "todas",
    tarefas: [
      {
        titulo: "Estudar ES6",
        finalizada: false,
      },
      {
        titulo: "Estudar SASS",
        finalizada: false,
      },
      {
        titulo: "Ir para a academia",
        finalizada: true,
      },
    ]
  })

  const tarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const tarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const tarefasFiltradas = () => {
    const { filtro } = estado

    switch (filtro) {
      case 'pendentes':
        return tarefasPendentes()
      case 'finalizadas':
        return tarefasFinalizadas()
      default: 
        return estado.tarefas
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }

    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = ""
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="tarefasPendentes().length" />
    <Formulario
      :cadastra-tarefa="cadastraTarefa"
      :tarefa-temp="estado.tarefaTemp" 
      :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value"
      :trocar-filtro="evento => estado.filtro = evento.target.value"
    />
    <ListaDeTarefas :tarefas="tarefasFiltradas()" />
  </div>
</template>