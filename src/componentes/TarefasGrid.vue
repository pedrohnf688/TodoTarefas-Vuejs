<template>
    <div class="tarefasgrid">
        <template v-if="tarefas.length">
            <Ta v-for="(tarefa, i) in tarefas" :key="tarefa.name" :tarefa="tarefa"
            @tarefaDeletada="$emit('tarefaDeletada', i)" @statusTarefa="$emit('statusTarefa', i)"></Ta>
        </template>
        <p v-else class="no-tarefas">Sua vida está em dia :)</p>
    </div>
</template>

<script>
import Ta from './Tarefa.vue'

export default {
    components: {Ta},
    props: {
        tarefas: {type: Array, required: true}
    }
}
</script>

<style>
.tarefasgrid {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

.tarefasgrid .tarefa {
    margin: 10px;
}

.no-tarefas {
    color: #AAA;
    font-size: 1.7rem;

}
</style>