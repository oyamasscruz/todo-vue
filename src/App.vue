<script setup>
  import { reactive } from 'vue';
  import HeaderDocument from './components/HeaderDocument.vue'
  import Forms from './components/Forms.vue'
  import List from './components/List.vue'

const estado = reactive({
  filtro: 'todas', //let's create a new estado to access the variables of the select
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizado: true,
    },
    {
      titulo: 'Estudar SSAS',
      finalizado: false,
    },
    {
      titulo: 'Estudar LESS',
      finalizado: true,
    },
    {
      titulo: 'Estudar GRUNT',
      finalizado: false,
    }
  ]
})

const getTarefasPendentes = () => { //this arrow function was created to return a VALUE(VALOR NUMERICO) of the tasks that doesen't done
  return estado.tarefas.filter(tarefa => !tarefa.finalizado) // we're filter the objects that it's not finish, or setting as false.
}

const getTarefasFinalizadas = () => { //this arrow function was created to return a VALUE(VALOR NUMERICO) of the tasks that its done
  return estado.tarefas.filter(tarefa => tarefa.finalizado) // we're filter the objects that it's finish, or setting as true.
}

const getTarefasFiltro = () => {
  const {filtro} = estado;
  switch(filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default: 
      return estado.tarefas;
  }
}

const cadastrarTarefa = () => {
  const novaTarefa = { // lets create a new object, and this way its gonna be right because the ways of the tarefas is a object
    titulo: estado.tarefaTemp,
    finalizado: false,
  }
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = '';
}
// after pass this function the novaTarefa wont be saved, because form has a property Defaul. It always refresh the page.
// Normaly we only can use this below, but the vue already has a shortcut to this, please see at @submit in form
// const cadastrarTarefa = (e) => {
//   e.preventDefault();
//   const novaTarefa = { // lets create a new object, and this way its gonna be right because the ways of the tarefas is a object
//     titulo: estado.tarefaTemp,
//     finalizado: false,
//   }
//   estado.tarefas.push(novaTarefa);
// }


// const cadastrarTarefa = () => {
//   return estado.tarefas.push(tarefaTemp) // this wont be work, because the ways of create a new task isnt this way
// }

</script>

<template>
  <div class="container">
    <HeaderDocument :pendentes-tarefas="getTarefasPendentes().length" /> 
    <!-- here, we have to claim the props we set in HeaderDocument ===> :pendentesTarefas -->
    <Forms :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastrar-tarefa="cadastrarTarefa"  />
    <List :get-tarefas-filtro="getTarefasFiltro()" :tarefas-pendentes="getTarefasPendentes().length"/>
  </div>
</template>