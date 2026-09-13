<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar color="primary">
        <ion-title>My Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <PhotoGalleryComponent />
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle } from '@ionic/vue';
import PhotoGalleryComponent from '../components/PhotoGalleryComponent.vue';
</script>