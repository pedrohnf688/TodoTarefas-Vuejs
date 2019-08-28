<template>
   <div class="progresso-tarefa">
       <span class="progresso-valor">{{prog}}%</span>
       <div class="progresso-bar" :style="{width: prog + '%'}"></div>

   </div>
</template>

<script>
export default {
    props: {
        prog:{type: Number, default: 0}
    }
}
</script>

<style>

.progresso-tarefa {
    position: relative;
    width: 80%;
    border: 1px solid #fff;
    color: #fff;
    border-radius: 8px;
    margin-bottom: 15px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.progresso-bar {
    position: absolute;
    border-radius: 8px;
    height: 100%;
    background-color: #4caf50;
    align-self: flex-start;
}
.progresso-valor {
    z-index: 1;
    font-size: 1.5rem;
}

</style>