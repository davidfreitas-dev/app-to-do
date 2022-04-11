<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button menu="main-menu" class="main-color"></ion-menu-button>
        </ion-buttons>
        <ion-title>Task Manager</ion-title>
        <ion-icon name="save" slot="end" class="ion-padding" @click="handleShowModal"></ion-icon>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <div id="container">
        <new-task @taskAdded="taskAdd"></new-task>
        <task-progress :progress="progress"></task-progress>
        <task-grid @taskDeleted="deleteTask" @taskStateChanged="toggleTaskState" :tasks="tasks"></task-grid>
        <modal-save ref="modal" @handleSave="handleSave"></modal-save>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { Storage } from '@capacitor/storage';
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButtons, IonIcon, IonMenuButton, } from '@ionic/vue';
import TaskProgress from '@/components/TaskProgress'
import NewTask from '@/components/NewTask'
import TaskGrid from '@/components/TaskGrid'
import ModalSave from '@/components/ModalSave'

export default ({
  name: 'HomePage',
  components: {
    IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButtons, IonIcon, IonMenuButton,
    TaskProgress, NewTask, TaskGrid, ModalSave
  },
  data() {
			return {
				tasks: [],
        lists: []
			}
		},
  computed: {
    progress() {
      const total = this.tasks.length
      const done = this.tasks.filter(t => !t.pending).length
      return Math.round(done / total * 100) || 0
    },
  },
  watch: {
    tasks: {
      deep: true,
      async handler() {
        await Storage.set({
          key: 'tasks',
          value: JSON.stringify(this.tasks)
        });
      }
    },
    lists: {
      deep: true,
      async handler() {
        await Storage.set({
          key: 'lists',
          value: JSON.stringify(this.lists)
        });
      }
    },
  },
  methods: {
    async getTasks() {
      const json = await Storage.get({ key: 'tasks' })
      const array = JSON.parse(json.value) || []
      this.tasks = Array.isArray(array) ? array : []
    },
    async getLists() {
      const json = await Storage.get({ key: 'lists' })
      const array = JSON.parse(json.value) || []
      this.lists = Array.isArray(array) ? array : []
    },
    taskAdd(task) {
      if (task.name != '') {
        const sameName = t => t.name === task.name
        const reallyNew = this.tasks.filter(sameName).length == 0
        if (reallyNew) {
          this.tasks.unshift({
            name: task.name,
            pending: task.pending || true
          })
        }
      } else {
        alert('Digite o nome da tarefa antes de adicionar')
      }
    },
    deleteTask(i) {
      this.tasks.splice(i, 1)
    },
    toggleTaskState(i) {
      this.tasks[i].pending = !this.tasks[i].pending
    },
    handleShowModal() {
      this.$refs.modal.showModal()
    },
    async handleSave(listName) {
      this.lists.unshift({
        id: this.lists.length + 1,
        name: listName,
        tasks: this.tasks
      })
    }
  },
  created() {
    this.getTasks();
    this.getLists();
  }
});
</script>

<style scoped>
#container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 1rem;
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;  
  color: #8c8c8c;  
  margin: 0;
}

#container a {
  text-decoration: none;
}

ion-icon {
  font-size: 1.3rem;
  color: var(--main);
}

@media only screen and (min-width: 550px) {
	ion-toolbar {
    width: 85%;
    margin: auto;
  }
}
@media only screen and (min-width: 768px) {
	ion-toolbar {
    width: 70%;
    margin: auto;
  }
}
</style>
