<template>
  <ion-fab vertical="bottom" horizontal="center" slot="fixed">
    <ion-fab-button @click="takePhoto">
      <ion-icon :icon="camera"></ion-icon>
    </ion-fab-button>
  </ion-fab>
</template>

<script setup lang="ts">
import { IonFab, IonFabButton, IonIcon } from '@ionic/vue';
import { camera } from 'ionicons/icons';
import { Camera, CameraResultType, CameraSource } from '@capacitor/camera';
import type { Photo } from '@capacitor/camera';

// This component ONLY triggers the camera and hands the result upward.
// It knows nothing about saving, loading, or displaying photos.
const emit = defineEmits<{
  (e: 'photo-taken', photo: Photo): void;
}>();

const takePhoto = async () => {
  try {
    const capturedPhoto = await Camera.getPhoto({
      resultType: CameraResultType.Uri,
      source: CameraSource.Camera, // opens the camera directly, no gallery/prompt option
      quality: 90,
    });

    emit('photo-taken', capturedPhoto);
  } catch (err) {
    // User cancelled the action sheet/camera - not a real error, just ignore
    console.log('Photo capture cancelled or failed:', err);
  }
};
</script>