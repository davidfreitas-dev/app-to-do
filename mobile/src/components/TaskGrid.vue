<template>
    <div class="wrapper">
        <div class="task__grid" v-if="tasks.length">
            <task-item v-for="(task, i) in tasks" :key="task.name" 
                @taskDeleted="$emit('taskDeleted', i)"
                @taskStateChanged="$emit('taskStateChanged', i)" 
                :task="task">
            </task-item>
        </div>
        <div v-else class="no__task">
            <span>Não há tarefas a serem ralizadas</span>
        </div>
    </div>
</template>

<script>
    import TaskItem from '@/components/TaskItem.vue'
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