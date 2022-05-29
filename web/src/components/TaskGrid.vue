<template>  
    <div class="tasks" :class="{ fullscreen: !tasks.length }">
        <template v-if="tasks.length">
            <Task v-for="(task, i) in tasks" :key="task.name" 
                @taskDeleted="$emit('taskDeleted', i)"
                @taskStateChanged="$emit('taskStateChanged', i)" 
                :task="task">
            </Task>
        </template>        
        <div v-else class="no-task">
            <span>Não há tarefas a serem ralizadas</span>
        </div>
    </div>
</template>

<script>
    import Task from './Task.vue'
    export default({
        components: { Task },
        props: {
            tasks: {
                type: Array,
                required: true
            }
        }
    })
</script>

<style>
	.tasks {
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        justify-items: center;
		margin: 1rem 0;
        width: 95%;
	}

    .no-task {
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
        font-size: 1rem;
        width: 100%;
    }

    .fullscreen {
        grid-template-columns: 100% !important;
    }

    @media screen and (max-width: 1024px) {
        .tasks {
            width: 100%;
            grid-template-columns: repeat(4, 1fr);
        }
    }

    @media screen and (max-width: 900px) {
        .tasks {
            width: 85%;
            grid-template-columns: repeat(3, 1fr);
        }
    }

    @media screen and (max-width: 500px) {
        .tasks {
            width: 90%;
            grid-template-columns: repeat(2, 1fr);
        }
    }
</style>