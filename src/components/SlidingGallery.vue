<template>
  <v-container fluid>
    <div class="image-container">
      <img
        v-for="(image, index) in images"
        :key="index"
        :src="image.src"
        :alt="image.alt"
        class="image"
      />
    </div>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      images: [], // Initialisiere das Array mit Bildern
    };
  },
  props: {
    pictureTaken: {
      type: Boolean,
      default: false,
    },
  },
  watch: {
    pictureTaken() {
      console.log("Picture Taken: ", this.pictureTaken);
      if (this.pictureTaken) {
        this.fetchImagesFromServer();
      }
    },
  },
  computed: {
    displayedImages() {
      const startIndex = Math.max(0, this.images.length - 9); // Index des ersten Bildes, das angezeigt werden soll
      return this.images.slice(startIndex); // Begrenze die angezeigten Bilder auf die letzten 12
    },
  },
  methods: {
    async fetchImagesFromServer() {
      try {
        const response = await axios.get(
          "https://cc-project-1-backend.azurewebsites.net/images"
        );
        const imagesData = response.data;
        console.log("Empfangene Daten:", imagesData);
        for (let imageData of imagesData) {
          if (imageData.url != undefined) {
            console.log("Bild-Daten:", imageData.url);
            (async () => {
              let imageResponse = await axios.get(imageData.url, {
                responseType: "blob",
              });
              // Bildobjekt erstellen
              const image = {
                src: URL.createObjectURL(imageResponse.data),
                alt: imageData.filename, // oder alternativen Alt-Text hier einfügen
              };
              // Bild zum Array hinzufügen
              this.images.push(image);
            })();
          }
        }
      } catch (error) {
        console.error("Fehler beim Abrufen der Bilder vom Server:", error);
      }
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
