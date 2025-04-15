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

<style>

.nav {
  display: flex;
  flex-direction: column;
}

.nav a {
  font-size: 1.2rem;
  display: flex;
  align-items: center;
  padding: 12px 0;
  color: #64748b;
}

.nav a.router-link-active,
.nav a:hover {
  color: inherit;
}

.nav a svg {
  width: 30px;
  margin-right: 30px;
}
</style>