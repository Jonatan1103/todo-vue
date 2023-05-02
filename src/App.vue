<script setup>
import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ tarefasPendentes().length }} tarefas pendentes
      </p>
    </header>

    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input 
            required
            :value="estado.tarefaTemp"
            @change="evento => estado.tarefaTemp = evento.target.value"
            type="text" 
            placeholder="Digite sua tarefa" 
            class="form-control"
          >
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select 
            @change="evento => estado.filtro = evento.target.value" 
            class="form-control"
          >
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in tarefasFiltradas()">
        <input
          @change="evento => tarefa.finalizada = evento.target.checked"
          :checked="tarefa.finalizada" 
          :id="tarefa.titulo" 
          type="checkbox"
        >
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>

</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
