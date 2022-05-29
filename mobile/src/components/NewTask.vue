<template>
    <div class="form">
        <input v-model="name" @keydown.enter="add" type="text" placeholder="Nome da Tarefa" />
        <button @click="add">
			<ion-icon name="add"></ion-icon>
		</button>
    </div>
</template>

<script>
import { IonIcon } from '@ionic/vue';

export default({
	components: {
		IonIcon,
	},
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

<style scoped>
    .form {
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 1rem;
		width: 90%;
	}

	.form input {
		width: 50%;
		height: 45px;
		padding: 0 15px;
		color: var(--font);
		font-size: 1rem;
		letter-spacing: .5px;
        outline: none;
		border: 1px solid var(--secondary);
		border-radius: 5px;
		border-top-right-radius: 0;
		border-bottom-right-radius: 0;
		background-color: var(--light);
	}

	.form button {
		height: 45px;
		border: none;
		padding: 0 15px;
		font-size: 1.5rem;
		font-weight: bold;
		border-radius: 5px;
		border-top-left-radius: 0;
		border-bottom-left-radius: 0;
		background-color: var(--main);
		cursor: pointer;
	}

	ion-icon {
		color: #fff;
	}

	@media screen and (max-width: 1024px) {
		.form input {
			width: 65%;
		}
	}

	@media screen and (max-width: 768px) {
		.form input {
			width: 70%;
		}
	}

	@media screen and (max-width: 550px) {
		.form input {
			width: 73%;
		}
	}
</style>