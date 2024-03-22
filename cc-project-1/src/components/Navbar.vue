<template>
  <nav>
    <v-toolbar app color="rgb(31, 31, 31)">
      <v-app-bar-nav-icon>
        <v-icon>mdi mdi-camera</v-icon>
      </v-app-bar-nav-icon>
      <v-toolbar-title class="text-uppercase">
        <span class="font-weight-light">Live Foto</span>
        <span class="font-weight-bold text-primary title"> Gallery </span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn>
        <a
          href="https://github.com/flo2274/cc-projekt-1"
          target="_blank"
          rel="noopener noreferrer"
        >
          <span class="font-weight-bold">Github</span>
          <v-icon right>mdi mdi-github</v-icon>
        </a>
      </v-btn>
    </v-toolbar>
  </nav>
</template>

<script>
import { mdiImage } from "@mdi/js";

export default {
  data() {
    return {
      icon: mdiImage,
    };
  },
};
</script>

<style>
a {
  text-decoration: none;
  color: inherit;
}

a:focus {
  color: inherit;
}
</style>
