<template>
  <ion-app>
    <ion-menu menuId="main-menu" content-id="main" side="start" type="overlay">
      <ion-header>
        <ion-toolbar>
          <ion-row class="ion-alignt-items-center">
            <ion-title>Task Manager</ion-title>
            <ion-row class="ion-justify-content-end ion-align-items-center">
              <ion-icon name="moon"></ion-icon>
              <ion-toggle class="themeToggle" @click="toggleTheme"></ion-toggle>
            </ion-row>
          </ion-row>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <ion-list>
          <ion-menu-toggle>
            <ion-item @click="$router.go(-1)">
              <ion-icon name="list" slot="start" class="main-color"></ion-icon>
              <ion-label>Listas Salvas</ion-label>
            </ion-item>
          </ion-menu-toggle>
          <ion-menu-toggle>
            <ion-item router-link="/">
              <ion-icon name="heart" slot="start" class="main-color"></ion-icon>
              <ion-label>Favoritas</ion-label>
            </ion-item>
          </ion-menu-toggle>
          <ion-menu-toggle>
            <ion-item router-link="/">
              <ion-icon name="trash" slot="start" class="main-color"></ion-icon>
              <ion-label>Lixeira</ion-label>
            </ion-item>
          </ion-menu-toggle>
        </ion-list>
      </ion-content>
      <ion-footer class="ion-padding">
        Task Manager v1.0
      </ion-footer>
    </ion-menu>
    <ion-router-outlet id="main"></ion-router-outlet>
  </ion-app>
</template>

<script>
import { IonApp, IonContent, IonMenu, IonHeader, IonToolbar, IonTitle, IonList, IonMenuToggle, IonItem, IonIcon, IonLabel, IonFooter, IonRouterOutlet, IonToggle, IonRow } from '@ionic/vue';

export default ({
  name: 'App',
  components: {
    IonApp, IonContent, IonMenu, IonHeader, IonToolbar, IonTitle, IonList, IonMenuToggle, IonItem, IonIcon, IonLabel, IonFooter, IonRouterOutlet, IonToggle, IonRow
  },
  methods: {
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
  }
});
</script>

<style scoped>
ion-toggle {
  --background: #c3c3c3;
  --background-checked: var(--hover-main);

  --handle-background: #fff;
  --handle-background-checked: var(--main);
}
ion-footer {
  color: var(--font);
}
</style>