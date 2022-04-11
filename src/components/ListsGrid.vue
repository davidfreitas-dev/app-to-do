<template>
    <ion-row class="ion-justify-content-center ion-align-items-center ion-padding">
        <ion-button class="btn-main" @click="handleNew">Nova Lista</ion-button>
    </ion-row>
    <ion-list v-if="lists.length">
        <ion-item v-for="(list, i) in lists" :key="i">
            <ion-label @click="handleSelect(list)">{{ list.name }}</ion-label>
        </ion-item>
    </ion-list>
</template>

<script>
import { Storage } from '@capacitor/storage';
import { IonRow, IonList, IonItem, IonLabel, IonButton } from '@ionic/vue';

export default {
    components: {
        IonRow, IonList, IonItem, IonLabel, IonButton
    },
    data() {
        return {
            lists: []
        }
    },
    methods: {
        async getLists() {
            const json = await Storage.get({ key: 'lists' })
            const array = JSON.parse(json.value) || []
            this.lists = Array.isArray(array) ? array : []
        },
        async getTasks() {
            const json = await Storage.get({ key: 'tasks' })
            const array = JSON.parse(json.value) || []
            const tasks = Array.isArray(array) ? array : []
            const lists = this.lists

            if (tasks.length && !lists.length) {
                this.$router.push('/tasks')
            }
        },
        async handleNew() {
            const tasks = []

            await Storage.set({
                key: 'tasks',
                value: JSON.stringify(tasks)
            });

            this.$router.push('/tasks')
        },
        async handleSelect(list) {
            await Storage.set({
                key: 'tasks',
                value: JSON.stringify(list.tasks)
            });

            this.$router.push('/tasks')
        }
    },
    created() {
        this.getLists()
        this.getTasks()
    }
}
</script>

<style>
.btn-main {
    --background: var(--main);
}
</style>