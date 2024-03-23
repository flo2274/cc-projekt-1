<template>
  <v-app>
    <Navbar />
    <v-main class="pa-3">
      <Stream
        @imageCaptured="onImageCaptured"
        :pictureTaken="takePicture"
        :cameraActive="cameraActive"
      />
      <v-container fluid>
        <v-row justify="center">
          <v-col cols="6" class="text-center">
            <v-btn
              color="primary"
              @click="toggleCamera"
              class="buttonToggleCamera"
              x-small
              >Toggle Camera</v-btn
            >
          </v-col>
          <v-col cols="6" class="text-center">
            <v-btn
              color="primary"
              @click="takeAPicture"
              class="buttonCaptureImage"
              x-small
              >Take Picture</v-btn
            >
          </v-col>
        </v-row>
      </v-container>
      <SlidingGallery :images="capturedImages" />
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
    onImageCaptured() {
      this.takePicture = false;
    },
  },
};
</script>

<style></style>
