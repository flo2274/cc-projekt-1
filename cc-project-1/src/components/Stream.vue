<template>
  <v-container fluid>
    <v-row justify="center">
      <v-col cols="12" md="6">
        <video ref="video" autoplay></video>
        <v-btn color="primary" @click="startCamera">Kamera starten</v-btn>
        <v-btn color="primary" @click="stopCamera">Kamera stoppen</v-btn>
        <v-btn color="primary" @click="captureImage">Bild aufnehmen</v-btn>
        <canvas ref="canvas" style="display: none"></canvas>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
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
      console.log("Aufgenommenes Bild:", imageDataURL);
    },
  },
};
</script>

<style>
/* Stildefinitionen hier hinzufügen, wenn benötigt */
</style>
