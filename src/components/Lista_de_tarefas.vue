<script setup>
    const props = defineProps(['tarefas'])
</script>

<template>
    <ul v-if="props.tarefas.length != 0" class="list-group mt-4">
        <li v-for="tarefa in props.tarefas" class="list-group-item">
            <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizado" type="checkbox" :id="tarefa.titulo">
            <label :class="{done: tarefa.finalizado}" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <p v-else>
        Você não tem tarefas pendentes
    </p>

</template>

<style scoped>
.done{
    text-decoration: line-through;
}
</style>