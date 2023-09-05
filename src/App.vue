<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaTarefas from './components/ListaTarefas.vue';
  

  const estado = reactive({

    filtro: 'todas',

    tarefaTemp: '',

    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Academia',
        finalizada: true,
      },
    ]
  })

  const getTarefasP = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
    
  }

  const getTarefasF = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
    
  }

  const filtro = () => {
    const {filtro} = estado;

    switch(filtro){
      case 'pendentes':
        return getTarefasP();
      case 'finalizadas':
        return getTarefasF();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado. tarefatemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefatemp = '';
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasP().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaTarefas :tarefas="filtro()"/>
  </div>
  </template>


