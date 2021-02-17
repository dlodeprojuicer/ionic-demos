<template>
  <ion-page class="mobile-only">
    <ion-header>
      <ion-toolbar>
        <ion-icon :icon="chevronBackOutline" @click="closeForm"></ion-icon>
          Detail
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding" :fullscreen="true">
      {{ data }}
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonIcon,
  IonContent
} from "@ionic/vue";

import { chevronBackOutline } from "ionicons/icons"

export default {
  name: 'MasterDetail',
  props: {
    data: {
      type: String
    },
    context: {
      type: Object
    },
    modalInstance: {
      type: Object
    },
  },
  components: {
    IonPage,
    IonHeader,
    IonToolbar,
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
    }
  }
}
</script>

<style scoped>
</style>
