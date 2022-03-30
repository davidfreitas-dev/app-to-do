<template>  
    <div class="tasks" :class="{ fullscreen: !tasks.length }">
        <template v-if="tasks.length">
            <task-item v-for="(task, i) in tasks" :key="task.name" 
                @taskDeleted="$emit('taskDeleted', i)"
                @taskStateChanged="$emit('taskStateChanged', i)" 
                :task="task">
            </task-item>
        </template>        
        <div v-else class="no-task">
            <span>Não há tarefas a serem ralizadas</span>
        </div>
    </div>
</template>

<script>
    import TaskItem from './TaskItem.vue'
    export default({
        components: { TaskItem },
        props: {
            tasks: {
                type: Array,
                required: true
            }
        }
    })
</script>

<style scoped>
	.tasks {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        justify-items: center;
		margin: 1rem 0;
        width: 60%;
	}

    .no-task {
        display: flex;
        justify-content: center;
        align-items: center;
        color: var(--font);
        font-size: 1rem;
        width: 100%;
    }

    .fullscreen {
        grid-template-columns: 100% !important;
    }

    @media screen and (max-width: 1024px) {
        .tasks {
            width: 80%;
        }
    }

    @media screen and (max-width: 900px) {
        .tasks {
            width: 75%;
            grid-template-columns: repeat(3, 1fr);
        }
    }

    @media screen and (max-width: 500px) {
        .tasks {
            width: 85%;
            grid-template-columns: repeat(2, 1fr);
        }
    }
</style>