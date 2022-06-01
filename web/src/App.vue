<template>
	<div id="app">
		<main>
			<h1>Lista de Tarefas</h1>
			<TaskProgress :progress="progress"/>
			<NewTask @taskAdded="taskAdd"/>
			<TaskGrid @taskDeleted="deleteTask" @taskStateChanged="toggleTaskState" :tasks="tasks"/>
		</main>
	</div>
</template>

<script>
	import TaskProgress from './components/TaskProgress.vue'
    import TaskGrid from './components/TaskGrid.vue'
	import NewTask from './components/NewTask.vue'

	export default {
		components: { TaskProgress, NewTask, TaskGrid },
		data() {
			return {
				tasks: []
			}
		},
		computed: {
			progress() {
				const total = this.tasks.length
				const done = this.tasks.filter(t => !t.pending).length
				return Math.round(done / total * 100) || 0
			}
		},
		watch: {
			tasks: {
				deep: true,
				handler() {
					localStorage.setItem('tasks', JSON.stringify(this.tasks))
				}
			}
		},
		methods: {
			taskAdd(task) {
				if (task.name != '') {
					const sameName = t => t.name === task.name
					const reallyNew = this.tasks.filter(sameName).length == 0
					if (reallyNew) {
						this.tasks.unshift({
							name: task.name,
							pending: task.pending || true
						})
					}
				} else {
					alert('Digite o nome da tarefa antes de adicionar')
				}
			},
			deleteTask(i) {
				this.tasks.splice(i, 1)
			},
			toggleTaskState(i) {
				this.tasks[i].pending = !this.tasks[i].pending
			}
		},
		created() {
			const json = localStorage.getItem('tasks')
			const array = JSON.parse(json) || []
			this.tasks = Array.isArray(array) ? array : []
		}
	}
</script>

<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
	
	body {
		color: var(--font);
		font-family: 'Poppins', sans-serif;
		background-color: var(--bg);
	}

	#app {
		display: flex;
		flex-direction: column;
		justify-content: top;
		align-items: center;
		height: 100vh;
	}

	main {
		width: 80%;
		display: flex;
		flex-direction: column;
		justify-content: top;
		align-items: center;
	}

	h1 {
		font-weight: 500;
		margin: 1.5rem 0 1rem 0;
	}

	@media screen and (max-width: 992px) {
		main {
			width: 90%;
		}
	}

	@media screen and (max-width: 768px) {
		main {
			width: 100%;
		}
	}
</style>
