<template>
  <ion-content class="ion-padding">
    <!-- Empty state -->
    <div v-if="photos.length === 0" class="empty-state">
      <ion-icon :icon="imagesOutline" class="empty-icon"></ion-icon>
      <h2>No photos yet</h2>
      <p>Tap the camera button below to take your first photo.</p>
    </div>

    <!-- Photo grid -->
    <ion-grid v-else>
      <ion-row>
        <ion-col size="6" size-md="4" v-for="(photo, index) in photos" :key="index">
          <ion-card class="photo-card" @click="removePhoto(index)">
            <ion-img :src="photo.webPath" />
          </ion-card>
        </ion-col>
      </ion-row>
    </ion-grid>

    <!-- CameraComponent only fires the shutter; this component just displays the result -->
    <CameraComponent @photo-taken="handlePhotoTaken" />
  </ion-content>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonContent,
  IonGrid,
  IonRow,
  IonCol,
  IonImg,
  IonCard,
  IonIcon,
} from '@ionic/vue';
import { imagesOutline } from 'ionicons/icons';
import type { Photo } from '@capacitor/camera';
import CameraComponent from './CameraComponent.vue';

// In-memory only - no filesystem/preferences persistence.
// Photos are lost on refresh/app restart.
const photos = ref<Photo[]>([]);

const handlePhotoTaken = (capturedPhoto: Photo) => {
  photos.value = [capturedPhoto, ...photos.value];
};

const removePhoto = (index: number) => {
  photos.value.splice(index, 1);
};
</script>

<style scoped>
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  height: 70vh;
  color: var(--ion-color-medium);
}

.empty-icon {
  font-size: 64px;
  margin-bottom: 12px;
  color: var(--ion-color-medium);
}

.empty-state h2 {
  margin: 0 0 4px;
  font-weight: 600;
  color: var(--ion-color-dark);
}

.empty-state p {
  margin: 0;
  font-size: 0.9rem;
  max-width: 240px;
}

.photo-card {
  margin: 0;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
}
</style>