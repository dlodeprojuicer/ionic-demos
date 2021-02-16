<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-button @click="closeForm">
          <ion-icon :icon="close"></ion-icon>
          <ion-title>Page One</ion-title>
        </ion-button>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding" :fullscreen="true">
      Modal
      <br /><br />
      
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonButton,
  IonIcon,
  IonTitle,
  IonContent
} from "@ionic/vue";

import { close } from "ionicons/icons"

export default {
  name: 'ModalTwo',
  props: {
    data: {
      type: Object
    },
    context: {
      type: Object
    },
    modalInstance: {
      type: Object
    }
  },
  components: {
    IonPage,
    IonHeader,
    IonToolbar,
    IonButton,
    IonIcon,
    IonTitle,
    IonContent,
  },
  setup() {
    return {
      close
    }
  },
  data() {
    return {
    }
  },
  methods: {
    closeForm() {
      // this.$ionic.modalController.dismiss();
      this.modalInstance.dismiss();
    }
  }
}
</script>

<style scoped>
</style>
