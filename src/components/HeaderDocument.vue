<script setup>
    const props = defineProps(['pendentesTarefas']) 
</script>
<!-- we dont have acess to java code in app.vue, so here we're gonna set new proprierties(props), to use here and link with the code in app.vue -->
<template>
    <header class="pd-5 mt-4 rounded-3 bg-light">
        <h1>Minhas Tarefas</h1>
        <p>Você tem {{ props.pendentesTarefas }} tarefas pendentes</p>
    </header>
</template>

<!-- now we change the function JS (getTarefasPendentes) and use the props to retrive latter in app.vue only the props-->