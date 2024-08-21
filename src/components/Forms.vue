<script setup>
    const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <!-- lets create a props for this function @submit.prevent = cadastrarTarefa -->
    <!-- we can set as cadastrarTarefa to make the call more easy -->
    <form @submit.prevent="props.cadastrarTarefa" class="form-control">
        <div class="row">
            <div class="col">
                <!-- here we have to create 2 props, one for access for tarefaTemp -->
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required
                    class="form-control" type="text">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <!-- lets retrieve the value of the toolbar of select. Remember always any value it will be : target.value, if the parameter its the evento so, ti will be evento.target.value -->
                <select @change="props.trocarFiltro" class="form-control">
                    <!-- so if we are setting the evento as an parameter, so its him that its gonna show for us. -->
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
    <!-- here we gonna test the arrow function and the retrive of function -->
    <!-- {{ estado.filtro }} -->
</template>