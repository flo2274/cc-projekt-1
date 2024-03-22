<template>
  <v-app>
    <Navbar />
    <v-main>
      <!-- <HelloWorld /> -->
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import AppFooter from "./components/AppFooter.vue";
import Navbar from "./components/Navbar.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    AppFooter,
    Navbar,
  },
};
</script>
