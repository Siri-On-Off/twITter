<script setup>
import LoginInfo from "../components/LoginInfo.vue";
import Composer from "../components/Composer.vue";
import Tweet from "../components/Tweet.vue";
import { onMounted, ref } from 'vue'
import { fetchStream } from '../api/requests'

const loading = ref(true)
const tweets = ref([]) 

onMounted(async () => {
  loading.value = true
    try {
        const stream = await fetchStream()
        
        tweets.value = stream
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
      v-for="tweet in tweets"
      :key="tweet.id"
      :user="{ id: tweet.id, name: tweet.name }"
      :text="tweet.text"
      :createdAt="tweet.created_at"
    />
  </section>

  <div class="loading" v-if="loading">
    Lade Tweets...
  </div>
</template>
