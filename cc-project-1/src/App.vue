<template>
  <v-app>
    <Navbar />
    <v-main>
      <Stream @imageCaptured="onImageCaptured" />
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
      capturedImages: [],
    };
  },
  methods: {
    onImageCaptured(imageDataURL) {
      this.capturedImages.push(imageDataURL); // Aufgenommenes Bild zur Liste der aufgenommenen Bilder hinzufügen
    },
  },
};
</script>
