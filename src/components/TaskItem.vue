<template>
    <div class="task animate__animated animate__fadeIn" :class="stateClass" @click="$emit('taskStateChanged', task)">
        <span @click.stop="$emit('taskDeleted', task)" class="close">
            <ion-icon name="close-outline"></ion-icon>
        </span>
        <small>{{ task.name }}</small>
    </div>
</template>

<script>
import { IonIcon } from '@ionic/vue';

export default {
    props: {
        task: { type: Object, required: true }
    },
    components: {
        IonIcon,
    },
    computed: {
        stateClass() {
            return {
                pending: this.task.pending,
                done: !this.task.pending
            }
        }
    }
}
</script>

<style scoped>
	.task {
		display: flex;
		justify-content: center;
		align-items: center;
        position: relative;
		margin: .5rem;
		width: 180px;
		height: 75px;
		border-radius: 5px;
        user-select: none;
        cursor: pointer;
	}

    .task small {
        color: #f1f1f1;
        text-shadow: 1px 1px 2px var(--shadow);
		font-size: 1.1rem;
        font-weight: 500;
        line-height: 1.3rem;
        text-align: center;
        max-width: 75%;
    }

	.pending {		
		border-left: 7px solid #da4e5e;
		background-color: var(--danger);
	}

	.done {		
		border-left: 7px solid #37a188;
		background-color: var(--main);
		text-decoration: line-through
	}

    .pending .close {
        color: #f1f1f1;
        background-color: #da4e5e;
    }

    .done .close {
        color: #f1f1f1;
        background-color: #37a188;
    }

    .close {        
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        top: 5px;
        right: 5px;
        width: 20px;
        height: 20px;
        font-size: 1rem;
        border-radius: 10px;
    }

    .close::before {
        margin-top: 5px;
    }

    ion-icon {
		color: #fff;
	}

    @media screen and (max-width: 768px) {
        .task {
            height: 60px;
            width: 140px;
        }

        .task small {
            font-size: 1.1rem;
        }
    }
</style>