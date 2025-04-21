<script setup>
  import { reactive } from "vue";
  import Cabecalho from "./components/cabecalho.vue"
  import Formulario from "./components/formulario.vue"
  import List from "./components/list.vue"

  

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
     
    ]
  })

  const getTarefasPendentes = () => {
    //Filtra as tarefas com o valor finaliza === false (!tarefa)
    console.log(estado.tarefas.filter(tarefa => !tarefa.finalizada))
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
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :cadastra-tarefa="cadastraTarefa" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" />
    <List :tarefas="estado.tarefas" :tarefas-filtradas="getTarefasFiltradas()"/>
  </div>
  
</template>

