<template>
    <div class="wrapper">
        <div class="task__grid" v-if="tasks.length">
            <Task v-for="(task, i) in tasks" :key="task.name" 
                @taskDeleted="$emit('taskDeleted', i)"
                @taskStateChanged="$emit('taskStateChanged', i)" 
                :task="task">
            </Task>
        </div>
        <div v-else class="no__task">
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