<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-icon :icon="chevronBackOutline" @click="closeForm"></ion-icon>
          Modal One
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding" :fullscreen="true">
      <h1>Modal One</h1>
      <ion-button expand="full" @click="openModalTwo">Open Two</ion-button>
      <ion-button expand="full" @click="openModalThree">Open Three</ion-button>
      <ion-button @click="presentActionSheet">Show Action Sheet</ion-button>
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

import ModalTwo from "./ModalTwo";
import ModalThree from "./ModalThree";

import { chevronBackOutline, caretForwardCircle, close, heart, trash, share } from "ionicons/icons"

export default {
  name: 'ModalOne',
  props: {
    data: {
      type: Object
    },
    context: {
      type: Object
    },
    modalInstance: {
      type: Object
    },
    actionSheetInstance: {
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
    async openModalTwo(ticket) {
      const modalInstance = modalController;
      const modal = await modalInstance
        .create({
          component: ModalTwo,
          componentProps: {
            context: this,
            data: ticket,
            modalInstance,
          },
        })

      return modal.present();
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
    async presentActionSheet() {
      const actionSheet = await this.actionSheetInstance.create({
        header: "Albums",
        cssClass: "my-custom-class",
        buttons: [
          {
            text: "Delete 2",
            role: "destructive",
            icon: trash,
            handler: () => {
              console.log("Delete clicked");
            },
          },
          {
            text: "Share",
            icon: share,
            handler: () => {
              console.log("Share clicked");
            },
          },
          {
            text: "Play (open modal)",
            icon: caretForwardCircle,
            handler: () => {
              console.log("Play clicked");
            },
          },
          {
            text: "Favorite",
            icon: heart,
            handler: () => {
              console.log("Favorite clicked");
            },
          },
          {
            text: "Cancel",
            icon: close,
            role: "cancel",
            handler: () => {
              console.log("Cancel clicked");
            },
          },
        ],
      });
      return actionSheet.present();
    },
  }
}
</script>

<style scoped>
</style>
