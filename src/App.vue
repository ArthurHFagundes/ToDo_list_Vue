<script setup> // SCRIPT
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :cadastra-tarefa="cadastraTarefa" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :trocar-filtro="evento => estado.filtro = evento.target.value"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>