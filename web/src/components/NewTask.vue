<template>
    <div class="form">
        <input v-model="taskName" @keydown.enter="add" type="text" placeholder="nome da tarefa" />
        <button @click="add">+</button>
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
            this.$emit('taskAdded', { name: this.taskName })            
            this.taskName = null
        }
    }
})
</script>

<style>
    .form {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 93%;
        padding: .5rem;
		margin-top: 1rem;
	}

	.form input {
		width: 65%;
		height: 45px;
		padding: 0 15px;
		color: #6c6c6c;
		font-size: 1rem;
		letter-spacing: .75px;
        outline: none;
		border: none;
		border-radius: 5px;
		border-top-right-radius: 0;
		border-bottom-right-radius: 0;
	}

	.form button {
		height: 45px;
		border: none;
		padding: 0 15px;
		color: white;
		font-size: 2rem;
		border-radius: 5px;
		border-top-left-radius: 0;
		border-bottom-left-radius: 0;
		background-color: lightseagreen;
		cursor: pointer;
	}

	@media screen and (max-width: 768px) {
		.form input {
			width: 75%;
		}
	}

	@media screen and (max-width: 550px) {
		.form input {
			width: 100%;
		}
	}
</style>