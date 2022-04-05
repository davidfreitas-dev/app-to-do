<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button menu="main-menu" class="main-color"></ion-menu-button>
        </ion-buttons>
        <ion-title>Task Manager</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <div id="container">
        <list-grid></list-grid>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButtons, IonMenuButton, } from '@ionic/vue';
import ListGrid from '../components/ListGrid.vue'

export default ({
  name: 'HomePage',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButtons,   
    IonMenuButton,
    ListGrid
  },
  data() {
    return {
      
    }
  },
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
