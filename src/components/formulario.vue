<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
     <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input required v-model="props.tarefaTemp" @change="props.editaTarefaTemp" type="text" placeholder="Digite a descrição da tarefa" class="form-control"></input>
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">
                Cadastrar
                </button>
            </div>
            <div class="col-md-2 me-4">
                <select @change="props.trocarFiltro" class="form-control">
                <option value="todas">Todas Tarefas</option>
                <option value="finalizadas">Finalizadas</option>
                <option value="pendentes">Pendentes</option>
                </select>
            </div>
        </div>
    </form>
</template>