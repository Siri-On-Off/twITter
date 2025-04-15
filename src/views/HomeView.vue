<script setup>
import LoginInfo from "../components/LoginInfo.vue";
import Composer from "../components/Composer.vue";
import Tweet from "../components/Tweet.vue";
import { onMounted } from 'vue';
import { ref } from 'vue';
import { fetchStream } from '../api/requests'

const loading = ref(true)

onMounted(async () => {
  loading.value = true
    try {
        const stream = await fetchStream()
        
        console.log('Stream geladen', stream)
    } catch (error) {
        console.error(error)
    } finally {
        loading.value = false
    }
})
</script>

<template>
  <LoginInfo />
  <Composer />

  <!-- Stream -->
  <section class="stream" v-if="!loading">
    <Tweet
      v-for="tweet in [1, 2, 3, 4, 5, 6, 7, 8, 9]"
      :user="{ id: 1, name: 'John Doe' }"
      :text="'Lorem ipsum dolor med'"
      :createdAt="'2023-01-01T12:00:00Z'"
    />
  </section>

  <div class="loading">
    Lade Tweets...
  </div>
</template>
