<template>
    <div class="task animate__animated animate__fadeIn" :class="stateClass" @click="$emit('taskStateChanged', task)">
        <span @click.stop="$emit('taskDeleted', task)" class="close">
            <ion-icon name="close-outline"></ion-icon>
        </span>
        <small>{{ task.name }}</small>
    </div>
</template>

<script>
export default {
    props: {
        task: { type: Object, required: true }
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

<style>
	.task {
		display: flex;
		justify-content: center;
		align-items: center;
        position: relative;
		margin: .5rem;
		width: 180px;
		height: 75px;
		border-radius: 5px;
        cursor: pointer;
        user-select: none;
	}

    .task small {
        max-width: 75%;
		font-size: 1.1rem;
        font-weight: 500;
        line-height: 1.3rem;
        text-align: center;
    }

	.pending {		
		border-left: 7px solid rgb(245, 38, 38);
		background-color: tomato;
	}

	.done {		
		border-left: 7px solid seagreen;
		background-color: rgb(52, 170, 103);
		text-decoration: line-through
	}

    .pending .close {
        background-color: rgb(245, 38, 38);
    }

    .done .close {
        background-color: seagreen;
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