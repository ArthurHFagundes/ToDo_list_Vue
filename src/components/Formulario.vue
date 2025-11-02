<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'editaTarefaTemp', 'trocarFiltro'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa()"> <!-- .prevent para prevenir o comportamento padrão -->
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required
                    class="form-control" type="text" placeholder="Digite sua nova tarefa"></input>
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">
                    Adicionar
                </button>
            </div>
            <div class="col-md-2">
                <!-- @açãoDeMudança="nomeDoEvento => objeto.atributoDoObjeto = nomeDoEvento.target.value"   -->
                <select @change="props.trocarFiltro" class="form-control">
                    <!-- armazena a informação do select -->
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>