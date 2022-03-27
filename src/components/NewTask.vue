<template>
    <div class="form">
        <input v-model="name" @keydown.enter="add" type="text" placeholder="nome da tarefa" />
        <button @click="add">
			<ion-icon name="add"></ion-icon>
		</button>
    </div>
</template>

<script>
export default({
    data() {
        return {            
            name: ''
        }
    },
    methods: {
        add() {
            this.$emit('taskAdded', {name: this.name})            
            this.name = ''
        }
    }
})
</script>

<style>
    .form {
		display: flex;
		justify-content: center;
		align-items: center;
        padding: .5rem;
		margin-top: 1rem;
		width: 90%;
	}

	.form input {
		width: 40%;
		height: 45px;
		padding: 0 15px;
		color: var(--font);
		font-size: 1rem;
		letter-spacing: .5px;
        outline: none;
		border: none;
		border-radius: 5px;
		border-top-right-radius: 0;
		border-bottom-right-radius: 0;
		background-color: var(--secondary);
	}

	.form button {
		height: 45px;
		border: none;
		padding: 0 15px;
		color: white;
		font-size: 1.5rem;
		font-weight: bold;
		border-radius: 5px;
		border-top-left-radius: 0;
		border-bottom-left-radius: 0;
		background-color: var(--main);
		cursor: pointer;
	}

	@media screen and (max-width: 768px) {
		.form input {
			width: 65%;
		}
	}

	@media screen and (max-width: 550px) {
		.form input {
			width: 100%;
		}
	}
</style>