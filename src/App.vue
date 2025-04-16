<script setup>
import { reactive } from "vue";

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: true
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false
      },
      {
        titulo: 'Ir para a Academia',
        finalizada: false
      },
    ]
  })

  const getTarefasPendentes = () => {
    //Filtra as tarefas com o valor finaliza === false (!tarefa)
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    //Filtra as tarefas com o valor finaliza === true
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const cadastraTarefa = () => {
  const item = {
    titulo: estado.tarefaTemp,
    finalizada: false
  }
  estado.tarefas.push(item)
  estado.tarefaTemp = ''
}


  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes()
      case 'finalizadas':
        return getTarefasFinalizadas()
      default:
        return estado.tarefas;
    }
  }


</script>

<template>
  
  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Minhas Tarefas</h1>
    <p>
      Você possui {{ getTarefasPendentes().length }} tarefas pendentes
    </p>
  </header>
  <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col">
        <input required v-model="estado.tarefaTemp" type="text" placeholder="Digite a descrição da tarefa" class="form-control"></input>
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary">
          Cadastrar
        </button>
      </div>
      <div class="col-md-2 me-4">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas Tarefas</option>
          <option value="finalizadas">Finalizadas</option>
          <option value="pendentes">Pendentes</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
      <label :class="{done: tarefa.finalizada === true}" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</template>

<style scoped>

.done{
  text-decoration: line-through;
}



</style>
