<template>
	<div id="app">
		<main>
			<h1>Lista de Tarefas</h1>
			<NewTask @taskAdded="taskAdd"/>
			<TaskProgress :progress="progress"/>
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