<template>
	<div id="app">
		<h1>Tarefas</h1>
		<TarefaProgress :prog="progresso"></TarefaProgress>
		<NewTarefa @tarefaAdicionada="addTarefa"/>
		<TGrid @tarefaDeletada="deletarTarefa" :tarefas="tarefas"
		       @statusTarefa="alterarStatusTarefa"></TGrid>
	</div>
</template>

<script>
import TarefaProgress from './componentes/TarefaProgress.vue'
import NewTarefa from './componentes/AddTarefa.vue'
import TGrid from './componentes/TarefasGrid.vue'

export default {
	components: {TarefaProgress, NewTarefa, TGrid},
	data(){
		return{
			 tarefas: []
		}
	},

	watch: {
		tarefas: {
			deep:true,
			handler(){
				localStorage.setItem('tarefas', JSON.stringify(this.tarefas))
			}
		}
	},
	
	computed:{
		progresso(){
			const total = this.tarefas.length
			const done = this.tarefas.filter(t => !t.status).length
			return Math.round(done / total * 100) || 0
		}
	},

	methods: {
		addTarefa(tarefa){
			const sameName = t => t.name === tarefa.name
			const reallyNew = this.tarefas.filter(sameName).length == 0

			if(reallyNew){
				this.tarefas.push({
				name:tarefa.name, 
				status: tarefa.status || true})
			}	
		},
		deletarTarefa(i){
			this.tarefas.splice(i, 1)
		},
		alterarStatusTarefa(i){
			this.tarefas[i].status = !this.tarefas[i].status
		}
	},

	created(){
		const json = localStorage.getItem('tarefas')
		const array = JSON.parse(json)
		this.tarefas = Array.isArray(array) ? array : []

	}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
