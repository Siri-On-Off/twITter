<script setup>
import { RouterLink } from 'vue-router'  
import IconLogin from './icons/IconLogin.vue'
import IconHome from './icons/IconHome.vue'
</script>

<template>
  <nav class="nav">
    <RouterLink to="/">
      <IconHome />
      Stream
    </RouterLink>
    <RouterLink to="/login">
      <IconLogin />
      Login
    </RouterLink>
  </nav>
</template>