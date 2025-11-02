<script setup> // SCRIPT
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefa: [
      {
        Titulo: "Estudar",
        Finalizada: false,
      },
      {
        Titulo: "Ver aula do curso",
        Finalizada: false,
      },
      {
        Titulo: "Ir para a Academia",
        Finalizada: true,
      },
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefa.filter(tarefa => !tarefa.Finalizada) // vai em "estado", filtra o array "tarefa", verifica se o atributo "Finalizada" é false 
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefa.filter(tarefa => tarefa.Finalizada) // vai em "estado", filtra o array "tarefa", verifica se o atributo "Finalizada" é true 
  }

  const getTarefasFiltradas = () => {
    const filtro = estado.filtro; // ou " const {filtro} = estado; "

    switch (filtro) {
      case 'pendentes': return getTarefasPendentes();
      case 'finalizadas': return getTarefasFinalizadas();
      default: return estado.tarefa;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      Titulo: estado.tarefaTemp, // nome
      Finalizada: false,
    }
    estado.tarefa.push(tarefaNova) // para jogar essas informações no array dentro de "estado"
    estado.tarefaTemp = ''
  }

</script>

<template> <!-- HTML -->
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1> Minhas Tarefas </h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes.
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa()"> <!-- .prevent para prevenir o comportamento padrão -->
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required class="form-control" type="text" placeholder="Digite sua nova tarefa"></input>
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">
            Adicionar
          </button>
        </div>
        <div class="col-md-2"> <!-- @açãoDeMudança="nomeDoEvento => objeto.atributoDoObjeto = nomeDoEvento.target.value"   -->
          <select @change="evento => estado.filtro = evento.target.value" class="form-control"> <!-- armazena a informação do select -->
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4" v-for="tarefa in getTarefasFiltradas()"><!-- lista objeto tarefa dentro do filtro  -->
      <li class="list-group-item">
        <input @change="evento => tarefa.Finalizada = evento.target.checked" :checked="tarefa.Finalizada" :id="tarefa.Titulo" type="checkbox" > <!-- :checked="tarefa.Finalizada" se for 'True' parece como checked -->
        <label :class="{ done: tarefa.Finalizada }" class="ms-3" :for="tarefa.Titulo">
          {{ tarefa.Titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped> /* CSS */

  .done {
    text-decoration: line-through;
  }

</style>
