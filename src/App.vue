<script setup>

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui 7 tarefas pendentes
      </p>
    </header>

    <form>
      <div class="row">
        <div class="col">
          <input type="text" placeholder="Digite sua tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item">
        <input type="checkbox">
        <label class="ms-3" for="">
          Estudar ES6
        </label>
      </li>
    </ul>
  </div>

</template>

<style scoped>

</style>
