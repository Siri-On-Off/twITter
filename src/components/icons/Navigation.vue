<script setup>
import { RouterLink } from 'vue-router'  
import IconLogin from './IconLogin.vue'
import IconHome from './IconHome.vue'
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