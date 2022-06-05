<template>
    <div class="task animate__animated animate__fadeIn"
        :class="stateClass" @click="$emit('taskStateChanged', task)">
        <span @click.stop="$emit('taskDeleted', task)" class="close">
            <ion-icon name="close-outline"></ion-icon>
        </span>
        {{ task.name }}
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