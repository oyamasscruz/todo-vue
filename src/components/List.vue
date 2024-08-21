<script setup>
    const props = defineProps(['getTarefasFiltro', 'tarefasPendentes'])
</script>
<template>
    <ul class="list-group mt-4" v-if="props.tarefasPendentes > 0">
        <li class="list-group-item" v-for="tarefa in props.getTarefasFiltro">
            <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado"
                :id="tarefa.titulo" type="checkbox">
            <!-- to add a class conditional, use simple mustache and passe over the :bind class, the rule, and the condition -->
            <label :class="{ concluido: tarefa.finalizado }" class="ms-2" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <span v-else>Muito Bem!!!Você não tem Tarefas Pendentes</span>
</template>
<style scoped>
.concluido {
    text-decoration: line-through;
}
</style>

