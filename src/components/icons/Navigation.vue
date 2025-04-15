<script setup>
import IconLogin from './IconLogin.vue'
import IconHome from './IconHome.vue'
</script>

<template>
  <nav class="nav">
    <a href="#" class="router-link-active">
      <IconHome />
      Stream
    </a>
    <a href="#">
      <IconLogin />
      Login
    </a>
  </nav>
</template>