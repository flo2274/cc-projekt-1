<template>
  <v-container fluid>
    <v-carousel
      v-model="currentIndex"
      hide-delimiters
      hide-controls
      style="max-height: 500px; overflow: hidden"
    >
      <v-carousel-item v-for="(imageDataURL, index) in images" :key="index">
        <img
          :src="imageDataURL"
          alt="Aufgenommenes Bild"
          style="width: 100%; height: 100%"
        />
      </v-carousel-item>
    </v-carousel>
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
  data() {
    return {
      currentIndex: 0,
    };
  },
};
</script>

<style>
/* Stildefinitionen hier hinzufügen, wenn benötigt */
</style>
