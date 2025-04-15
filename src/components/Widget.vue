<script setup>
defineProps(['title'])
</script>

<template>
  <!-- Top User Widget -->
  <section class="widget">
    <h2 class="widget__heading">
    {{ title }}
    </h2>

    <!-- Hier wird der Inhalt des <Widget> Tags gerendert -->
    <slot />
  </section>
</template>
