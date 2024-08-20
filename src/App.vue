<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas', //let's create a new estado to access the variables of the select
  novaTarefa: '',
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
  const newTarefa = { // lets create a new object, and this way its gonna be right because the ways of the tarefas is a object
    titulo: estado.novaTarefa,
    finalizado: false,
  }
  estado.tarefas.push(newTarefa);
  estado.novaTarefa = '';
}
// after pass this function the newTarefa wont be saved, because form has a property Defaul. It always refresh the page.
// Normaly we only can use this below, but the vue already has a shortcut to this, please see at @submit in form
// const cadastrarTarefa = (e) => {
//   e.preventDefault();
//   const newTarefa = { // lets create a new object, and this way its gonna be right because the ways of the tarefas is a object
//     titulo: estado.novaTarefa,
//     finalizado: false,
//   }
//   estado.tarefas.push(newTarefa);
// }


// const cadastrarTarefa = () => {
//   return estado.tarefas.push(novaTarefa) // this wont be work, because the ways of create a new task isnt this way
// }
</script>

<template>
  <div class="container">
    <header class="pd-5 mt-4 rounded-3 bg-light">
      <h1>Minhas Tarefas</h1>
      <p>Você tem {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form  @submit.prevent="cadastrarTarefa" class="form-control">
      <div class="row">
        <div class="col">
          <input :value="estado.novaTarefa" @change="evento => estado.novaTarefa = evento.target.value" required class="form-control" type="text">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <!-- lets retrieve the value of the toolbar of select. Remember always any value it will be : target.value, if the parameter its the evento so, ti will be evento.target.value -->
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <!-- so if we are setting the evento as an parameter, so its him that its gonna show for us. -->
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <!-- here we gonna test the arrow function and the retrive of function -->
    {{ estado.filtro }}
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for ="tarefa in getTarefasFiltro()">
        <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
        <!-- to add a class conditional, use simple mustache and passe over the :bind class, the rule, and the condition -->
        <label :class="{ concluido: tarefa.finalizado }" class="ms-2" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.concluido {
  text-decoration: line-through;
}
</style>
