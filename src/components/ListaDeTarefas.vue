<script setup>
    const props = defineProps(['tarefas']);
</script>

<template >
    <ul class="list-group mt-4" v-for="tarefa in props.tarefas"><!-- lista objeto tarefa dentro do filtro  -->
        <li class="list-group-item">
            <input @change="evento => tarefa.Finalizada = evento.target.checked" :checked="tarefa.Finalizada"
                :id="tarefa.Titulo" type="checkbox">
            <!-- :checked="tarefa.Finalizada" se for 'True' parece como checked -->
            <label :class="{ done: tarefa.Finalizada }" class="ms-3" :for="tarefa.Titulo">
                {{ tarefa.Titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped> /* CSS */
    .done {
        text-decoration: line-through;
    }
</style>