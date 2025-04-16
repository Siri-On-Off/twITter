<script setup>
import { RouterLink } from 'vue-router'  
import IconLogin from './icons/IconLogin.vue'
import IconHome from './icons/IconHome.vue'
import { computed } from 'vue';
import { useAuth } from '../api/auth'

// "logout" neu auch importieren.
const { isLoggedIn, logout } = useAuth()

// Logout-Funktion beim Klick ausführen
const handleLogout = () => {
  logout()  // ← führt Logout durch (und sollte isLoggedIn aktualisieren)
}
</script>

<template>
  <nav class="nav">
    <RouterLink to="/">
      <IconHome />
      Stream
    </RouterLink>
    <RouterLink to="/login" v-if="!isLoggedIn" >
      <IconLogin />
      Login
    </RouterLink>
    <a href="#" class="logout-link" v-else @click.prevent="handleLogout">
      <IconLogin />
      Logout
    </a>
  </nav>
</template>