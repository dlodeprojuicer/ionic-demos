<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-icon :icon="chevronBackOutline" @click="closeForm"></ion-icon>
          Modal Two
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding" :fullscreen="true">
      <h1>Modal Two</h1>
      <ion-button expand="full" @click="openModalThree">Open Three</ion-button>
      <ion-button expand="full" @click="openModalOne">Open One</ion-button>
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
  IonContent,
  modalController
} from "@ionic/vue";

import ModalOne from "./ModalOne";
import ModalThree from "./ModalThree";

import { chevronBackOutline } from "ionicons/icons"

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
    IonContent,
  },
  setup() {
    return {
      chevronBackOutline
    }
  },
  methods: {
    closeForm() {
      // this.$ionic.modalController.dismiss();
      this.modalInstance.dismiss();
    },
    async openModalThree(ticket) {
      const modalInstance = modalController;
      const modal = await modalInstance
        .create({
          component: ModalThree,
          componentProps: {
            context: this,
            data: ticket,
            modalInstance,
          },
        })

      return modal.present();
    },
    async openModalOne(ticket) {
      const modalInstance = modalController;
      const modal = await modalInstance
        .create({
          component: ModalOne,
          componentProps: {
            context: this,
            data: ticket,
            modalInstance,
          },
        })

      return modal.present();
    },
  }
}
</script>

<style scoped>
</style>
