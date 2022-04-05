<template>
    <ion-grid>
        <ion-row v-for="(list, i) in lists" :key="i">
            <ion-col>
                {{ list.name }}
            </ion-col>
        </ion-row>
    </ion-grid>
</template>

<script>
import { Storage } from '@capacitor/storage';
import { IonGrid, IonRow, IonCol } from '@ionic/vue';

export default {
    components: {
        IonGrid, IonRow, IonCol
    },
    data() {
        return {
            lists: null
        }
    },
    methods: {
        async getList() {
            const list = await Storage.get({ key: 'tasksList' })
            const array = JSON.parse(list.value)
            this.lists = array
        }
    },
    created() {
        this.getList()
    }
}
</script>

<style>

</style>