<template>
  <v-container fluid>
    <div class="image-container">
      <img
        v-for="(imageDataURL, index) in displayedImages"
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
    displayedImages() {
      const startIndex = Math.max(0, this.images.length - 12); // Index des ersten Bildes, das angezeigt werden soll
      return this.images.slice(startIndex); // Begrenze die angezeigten Bilder auf die letzten 12
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
