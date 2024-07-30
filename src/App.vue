<script setup>
import { RouterLink, RouterView } from "vue-router";

import Nav from "./components/Nav.vue";
import Footer from "./components/Footer.vue";
</script>

<template>
  <header>
    <Nav></Nav>
  </header>

  <RouterView />
  <footer>
    <Footer></Footer>
  </footer>
</template>

<style scoped></style>
