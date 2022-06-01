<template>
    <div class="task animate__animated animate__fadeIn" :class="stateClass" @click="$emit('taskStateChanged', task)">
        <span @click.stop="$emit('taskDeleted', task)" class="ti-close close"></span>
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
        text-shadow: 1px 1px 3px #666;
	}

    .task small {
        max-width: 75%;
		font-size: 1.3rem;
        font-weight: 500;
        line-height: 1.3rem;
        text-align: center;
    }

	.pending {
		background: var(--secondary);
	}

	.done {
		text-decoration: line-through;
		background: var(--primary);
	}

    .pending .close {
        background-color: #d64542;
    }

    .done .close {
        background-color: #269255;
    }

    .close {        
        display: flex;
        justify-content: center;
        align-content: center;   
        position: absolute;
        top: 5px;
        right: 5px;
        width: 20px;
        height: 20px;
        font-size: .65rem;
        border-radius: 10px;
    }

    .close::before {
        margin-top: 5px;
    }

    @media screen and (max-width: 768px) {
        .task {
            height: 60px;
            width: 155px;
        }

        .task small {
            font-size: 1.1rem;
        }
    }
</style>