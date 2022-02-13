<script setup>
import Footerarea from "@/components/global/Footerarea.vue";
import Navbar from "@/components/global/Navbar.vue";
import { RouterView } from "vue-router";
</script>

<template>
  <header>
    <Navbar />
  </header>

  <RouterView />

  <footer>
    <Footerarea />
  </footer>
</template>

<style></style>
