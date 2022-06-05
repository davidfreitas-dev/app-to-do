<template>
    <div class="task animate__animated animate__fadeIn"
        :class="stateClass" @click="$emit('taskStateChanged', task)">
        <span @click.stop="$emit('taskDeleted', task)" class="ti-close close"></span>
        {{ task.name }}
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