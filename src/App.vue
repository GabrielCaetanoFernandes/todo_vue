<script setup>
import { reactive } from 'vue';

  const estado = reactive({

    filtro: 'todas',

    tarefatemp: '',

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasP().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefatemp" @change="evento => estado.tarefatemp = evento.target.value" class="form-control" type="text" placeholder="Descrição da tarefa" required>
        </div>
        <div class="col-md-2">
          <button class="btn btn-outline-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in filtro()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
  </template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
