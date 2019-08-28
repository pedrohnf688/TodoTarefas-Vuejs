<template>
    <div class="tarefa"  @click="$emit('statusTarefa', tarefa)" :class="stateClass">
        <span class="close" @click.stop="$emit('tarefaDeletada', tarefa)">X</span>
        <p>{{tarefa.name}}</p>
    </div>
</template>

<script>
export default {
    props: {
        tarefa: {type: Object, required: true}
    },
    computed:{
        stateClass(){
            return{
                 tarefaPendente: this.tarefa.status,
                 tarefaFeita: !this.tarefa.status
            
            }
        }
    }
}
</script>

<style>
.tarefa {
    position: relative;
    box-sizing: border-box;
    width: 200px;
    height: 100px;
    padding: 10px;
    border-radius: 8px;
    font-size: 2rem;
    font-weight: 300;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
}

.tarefaFeita {
    color:#DDD;
    border-left: 12px solid #0a8f08;
    background-color: #4caf50;
    text-decoration: line-through;
}

.tarefaPendente {
    border-left: 12px solid #b73229;
    background-color: #f44336;
}

.tarefaPendente .close {
    background-color: #b73229;
}

.tarefaFeita .close {
    background-color: #0a8f08;
}

.close {
    position: absolute;
    right: 10px;
    top: 10px;
    font-size: 0.9rem;
    font-weight: 600;
    height: 20px;
    width: 20px;
    border-radius: 10px;
    display: flex;
    justify-content: center;
}

</style>
