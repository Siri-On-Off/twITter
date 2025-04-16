<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <RouterLink to="/" class="logo">
    Tw<strong>IT</strong>ter
  </RouterLink>
</template>

<style>

.logo {
  font-size: 2.6rem;
  font-weight: 500;
  padding: 20px 0;

  background: linear-gradient(to bottom, #fb7185, #e11d48);
  background-clip: text;
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.logo strong {
  font-weight: 800;
}
</style>