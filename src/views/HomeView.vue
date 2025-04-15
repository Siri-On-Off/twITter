<script setup>
import LoginInfo from "../components/icons/LoginInfo.vue";
import Composer from "../components/icons/Composer.vue";
import Tweet from "../components/icons/Tweet.vue";
</script>

<template>
  <LoginInfo />
  <Composer />

  <!-- Stream -->
  <section class="stream">
    <Tweet
      v-for="tweet in [1, 2, 3, 4, 5, 6, 7, 8, 9]"
      :user="{ id: 1, name: 'John Doe' }"
      :text="'Lorem ipsum dolor med'"
      :createdAt="'2023-01-01T12:00:00Z'"
    />
  </section>
</template>
