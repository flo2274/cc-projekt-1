<template>
  <v-container fluid>
    <video ref="video" height="100%" width="100%" autoplay></video>
  </v-container>
  <canvas ref="canvas" style="display: none"></canvas>
</template>

<script>
import axios from "axios";
export default {
  emits: ["imageCaptured"], // Deklariere das imageCaptured-Ereignis
  props: {
    pictureTaken: {
      type: Boolean,
      default: false,
    },
    cameraActive: {
      type: Boolean,
      default: false,
    },
  },
  watch: {
    pictureTaken() {
      console.log("Picture Taken: ", this.pictureTaken);
      if (this.pictureTaken) {
        this.captureImage();
      }
    },
    cameraActive() {
      console.log("Camera Active: ", this.cameraActive);
      if (this.cameraActive) {
        this.startCamera();
      } else {
        this.stopCamera();
      }
    },
  },
  methods: {
    async startCamera() {
      try {
        const stream = await navigator.mediaDevices.getUserMedia({
          video: true,
        });
        this.$refs.video.srcObject = stream;
      } catch (error) {
        console.error("Fehler beim Zugriff auf die Kamera:", error);
      }
    },
    stopCamera() {
      const stream = this.$refs.video.srcObject;
      const tracks = stream.getTracks();
      tracks.forEach((track) => track.stop());
      this.$refs.video.srcObject = null;
    },
    captureImage() {
      const video = this.$refs.video;
      const canvas = this.$refs.canvas;
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      canvas
        .getContext("2d")
        .drawImage(video, 0, 0, canvas.width, canvas.height);
      // Hier kannst du mit dem aufgenommenen Bild auf dem Canvas weiterarbeiten
      // Zum Beispiel kannst du das Bild in ein Daten-URL umwandeln und speichern oder anzeigen
      const imageDataURL = canvas.toDataURL("image/png");

      // this.$emit("imageCaptured", imageDataURL);-------

      this.sendImage(imageDataURL); // Sendet das Bild an den Server
      console.log("Bild aufgenommen:", imageDataURL);
    },

    async sendImage(imageDataURL) {
      try {
        // Sende das Bild per Axios an den Server
        const response = await axios.post(
          "https://cc-project-1-backend.azurewebsites.net/upload",
          {
            image: imageDataURL,
          }
        );
        console.log("Bild erfolgreich an den Server gesendet:", response.data);
      } catch (error) {
        console.error("Fehler beim Senden des Bildes an den Server:", error);
      }
    },
  },
};
</script>

<style>
video {
  width: 100%;
  height: calc(
    100vw * 9 / 16
  ); /* Berechnet die Höhe basierend auf dem Seitenverhältnis 16:9 */
}
</style>
