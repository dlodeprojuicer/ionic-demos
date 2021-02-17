
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons>
          <ion-button slot="start">
          <ion-back-button defaultHref="/"></ion-back-button>
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
				<ion-grid>
					<ion-row>
						<ion-col>
							<ion-list>
								<ion-item>
									<ion-label>
										<ion-icon slot="icon-only" :icon="menu">Show Settings</ion-icon>
										Master
									</ion-label>
								</ion-item>
								<ion-item v-for="(item, index) in list" :key="index" detail @click="showDetail(item)">
									<ion-label>{{ item.label }}</ion-label>
								</ion-item>
							</ion-list>
						</ion-col>
						<ion-col size="9" class="split-pane-desktop-only">
							<ion-item>
								<ion-label>
									Detail
								</ion-label>
							</ion-item>
							<p v-if="detail">
								{{ detail }}
							</p>
						</ion-col>
					</ion-row>
				</ion-grid>
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
  IonIcon,
	IonGrid,
	IonCol,
	IonRow,
	IonList,
	IonLabel,
	IonItem
} from "@ionic/vue";

import MasterDetail from "../components/MasterDetail";

import { caretForwardCircle, close, heart, trash, share, ellipsisVerticalSharp, menu } from "ionicons/icons";

export default {
  name: "split-pane",
  components: {
    IonPage,
    IonHeader,
    IonToolbar,
    IonContent,
    IonButton,
    IonButtons,
    IonBackButton,
    IonIcon,
		IonGrid,
		IonCol,
		IonRow,
		IonList,
		IonLabel,
		IonItem
  },
  setup() {
    return {
      caretForwardCircle, close, heart, trash, share,
      ellipsisVerticalSharp,
			menu
    }
  },
	data() {
		return {
			detail: null,
			list: [
				{
					label: "Item 1",
					detail: "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Repellat aliquam deserunt harum rem earum assumenda perspiciatis expedita. Aliquid distinctio tenetur fugiat qui recusandae obcaecati voluptates."
				},
				{
					label: "Item 2",
					detail: "Repellat aliquam deserunt harum rem earum assumenda perspiciatis expedita. Aliquid distinctio tenetur fugiat qui recusandae obcaecati voluptates."
				},
				{
					label: "Item 3",
					detail: "Aliquid distinctio tenetur fugiat qui recusandae obcaecati voluptates."
				}
			]
		}
	},
  methods: {
		async showDetail(item) {
			// document.documentElement.clientWidth => device size
			// anything > 420 is not mobile
			console.log(document.documentElement.clientWidth);
			if (document.documentElement.clientWidth > 420) {
				// if you have to have data when item is clicked
				// use item.id to fetch data
				// onSuccess assign data to this.detail
				this.detail = item.detail;
			} else {
				const modalInstance = modalController;
				const modal = await modalInstance.create({
					component: MasterDetail,
					componentProps: {
						context: this,
						data: item.detail,
						modalInstance,
					},
				});

				return modal.present();
			}
		}
  },
};
</script>
