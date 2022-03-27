<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-row class="ion-justify-content-between ion-align-items-center">
          <ion-row class="ion-align-items-center">
            <ion-buttons>
              <ion-menu-button menu="main-menu" class="main-color"></ion-menu-button>
            </ion-buttons>
            <ion-title>Task Manager</ion-title>
          </ion-row>
          <ion-row class="ion-justify-content-between ion-align-items-center">
              <ion-icon name="moon"></ion-icon>
              <ion-toggle class="themeToggle" @click="toggleTheme"></ion-toggle>
            </ion-row>
        </ion-row>        
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <div id="container">
        <task-progress :progress="progress"></task-progress>
        <new-task @taskAdded="taskAdd"></new-task>
        <task-grid @taskDeleted="deleteTask" @taskStateChanged="toggleTaskState" :tasks="tasks"></task-grid>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import TaskProgress from '@/components/TaskProgress'
import NewTask from '@/components/NewTask'
import TaskGrid from '@/components/TaskGrid'

export default ({
  name: 'HomePage',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,

    TaskProgress,
    NewTask,
    TaskGrid
  },
  data() {
			return {
				tasks: []
			}
		},
  computed: {
    progress() {
      const total = this.tasks.length
      const done = this.tasks.filter(t => !t.pending).length
      return Math.round(done / total * 100) || 0
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks))
      }
    }
  },
  methods: {
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
    loadColorsTheme() {
      const toggle = document.querySelector(".themeToggle");
      const prefersDark = window.matchMedia("(prefers-color-scheme: dark)");
      prefersDark.addEventListener("change", (e) => checkToggle(e.matches));
      checkToggle(prefersDark.matches);
      
      function checkToggle(shouldCheck) {
        toggle.checked = shouldCheck;
        document.documentElement.classList.toggle("dark");
      }
    },
    toggleTheme() {
      document.documentElement.classList.toggle("dark");
    },
  },
  created() {
    this.$nextTick(() => {
      this.loadColorsTheme();
    });
    
    const json = localStorage.getItem('tasks')
    const array = JSON.parse(json) || []
    this.tasks = Array.isArray(array) ? array : []
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

ion-title, ion-icon {
  color: var(--font);
}

ion-toggle {
  --background: #c3c3c3;
  --background-checked: var(--hover-main);

  --handle-background: #fff;
  --handle-background-checked: var(--main);
}
</style>
