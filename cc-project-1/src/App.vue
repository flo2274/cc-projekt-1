<template>
  <v-app>
    <Navbar />
    <v-main>
      <Stream
        @imageCaptured="onImageCaptured"
        :pictureTaken="takePicture"
        :cameraActive="cameraActive"
      />

      <SlidingGallery :images="capturedImages" />
      <v-btn color="primary" @click="toggleCamera" class="buttonStartCamera"
        >Toggle Camera</v-btn
      >
      <v-btn color="primary" @click="takeAPicture" class="buttonCaptureImage"
        >Bild aufnehmen</v-btn
      >
    </v-main>
  </v-app>
</template>

<script>
import SlidingGallery from "./components/SlidingGallery.vue";

export default {
  components: {
    SlidingGallery,
  },
  data() {
    return {
      cameraActive: false,
      takePicture: false,
      capturedImages: [],
    };
  },
  methods: {
    toggleCamera() {
      this.cameraActive = !this.cameraActive;
      console.log("Camera Active: ", this.cameraActive);
    },
    takeAPicture() {
      this.takePicture = true;
      console.log("Picture Taken: ", this.takePicture);
    },
    onImageCaptured(imageDataURL) {
      this.capturedImages.push(imageDataURL);
      this.takePicture = false;
    },
  },
};
</script>
