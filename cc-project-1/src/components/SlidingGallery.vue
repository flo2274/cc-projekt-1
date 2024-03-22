<template>
  <v-container fluid>
    <div class="image-container">
      <img
        v-for="(imageDataURL, index) in lastTenImages"
        :key="index"
        :src="imageDataURL"
        alt="Aufgenommenes Bild"
        class="image"
      />
    </div>
  </v-container>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    lastTenImages() {
      return this.images.slice(-12); // Begrenze die Anzahl der angezeigten Bilder auf die letzten 10
    },
  },
};
</script>

<style>
.image-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.image {
  width: 100px; /* Anpassen der Bildgröße */
  height: auto; /* Anpassen der Bildgröße */
  margin: 5px; /* Anpassen des Abstands zwischen den Bildern */
}
</style>
