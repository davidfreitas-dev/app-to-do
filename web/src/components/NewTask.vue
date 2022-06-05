<template>
	<div class="wrapper">
		<div class="input__container">
			<input type="text" placeholder="Nome da tarefa"
				v-model="taskName" @keydown.enter="add" />
			<button @click="add">+</button>
		</div>
	</div>
</template>

<script>
export default({
    data() {
        return {            
            taskName: null
        }
    },
    methods: {
        add() {
            const taskName = this.taskName.toLowerCase().replace(/(?:^|\s)\S/g, function(a) { return a.toUpperCase(); });
            this.$emit('taskAdded', { name: taskName })       
            this.taskName = null
        }
    }
})
</script>