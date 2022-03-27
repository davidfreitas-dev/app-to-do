<template>
  <ion-app>
    <ion-menu menuId="main-menu" content-id="main" side="start" type="overlay">
      <ion-header>
        <ion-toolbar>
          <ion-title>Task Manager</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <ion-list>
          <ion-menu-toggle>
            <ion-item router-link="/">
              <ion-icon name="save" slot="start"></ion-icon>
              <ion-label>Listas Salvas</ion-label>
            </ion-item>
          </ion-menu-toggle>
          <ion-menu-toggle>
            <ion-item router-link="/">
              <ion-icon name="heart" slot="start"></ion-icon>
              <ion-label>Favoritas</ion-label>
            </ion-item>
          </ion-menu-toggle>
          <ion-menu-toggle>
            <ion-item router-link="/">
              <ion-icon name="trash" slot="start"></ion-icon>
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
import { IonApp, IonRouterOutlet } from '@ionic/vue';

export default ({
  name: 'App',
  components: {
    IonApp,
    IonRouterOutlet
  }
});
</script>