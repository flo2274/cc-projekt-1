<template>
  <v-app>
    <Navbar />
    <v-main>
      <Stream />
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Navbar from "./components/Navbar.vue";
import Stream from "./components/Stream.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Navbar,
    Stream,
  },
};
</script>
