
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons>
          <ion-button slot="start">
          <ion-back-button defaultHref="/"></ion-back-button>
          </ion-button>
        </ion-buttons>
        <ion-buttons slot="end">
          <ion-button  @click="openPopover" slot="end">
            <ion-icon slot="icon-only" :icon="ellipsisVerticalSharp">Show Settings</ion-icon>
          </ion-button>         
        </ion-buttons>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <h1>Home page</h1>

      <ion-button expand="full" @click="openModal">Open Modal</ion-button>
      <ion-button @click="presentActionSheet">Show Action Sheet</ion-button>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonContent,
  IonButton,
  modalController,
  IonButtons,
  IonBackButton,
  actionSheetController,
  popoverController,
  IonIcon
} from "@ionic/vue";

import ModalOne from "../components/ModalOne";
import SettingsMenu from '../components/settings';

import { caretForwardCircle, close, heart, trash, share, ellipsisVerticalSharp } from "ionicons/icons";

export default {
  name: "Explorer",
  components: {
    IonPage,
    IonHeader,
    IonToolbar,
    IonContent,
    IonButton,
    IonButtons,
    IonBackButton,
    IonIcon
  },
  setup() {
    const actionSheetInstance = actionSheetController;
    return {
      caretForwardCircle, close, heart, trash, share,
      actionSheetInstance,
      ellipsisVerticalSharp
    }
  },
  methods: {
    async openPopover(ev) {
      const popover = await popoverController
        .create({
          component: SettingsMenu,
          cssClass: 'my-custom-class',
          event: ev,
          translucent: true
        });
      return popover.present();
    },
    async openModal(ticket) {
      const modalInstance = modalController;
      const modal = await modalInstance.create({
        component: ModalOne,
        componentProps: {
          context: this,
          data: ticket,
          modalInstance,
          actionSheetInstance: this.actionSheetInstance
        },
      });

      return modal.present();
    },
    async presentActionSheet() {
      const actionSheet = await this.actionSheetInstance.create({
        header: "Albums",
        cssClass: "my-custom-class",
        buttons: [
          {
            text: "Delete",
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
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
}
.logout {
  margin-right: 20px;
}

ion-icon {
  color: #fff;
}
</style>
