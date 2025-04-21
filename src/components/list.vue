<script setup>
    const props = defineProps(['tarefasFiltradas', 'tarefas'])
</script>

<template>
    <ul v-if="props.tarefas.length > 0" class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefasFiltradas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
            <label :class="{done: tarefa.finalizada === true}" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <span class="alert alert-primary d-flex mt-3" v-else-if="props.tarefas.length === 0">
        Não existem tarefas
    </span>
</template>

<style scoped>

    .done{
    text-decoration: line-through;
    }

</style>
