<script setup>
import LoginInfo from "../components/LoginInfo.vue";
import Composer from "../components/Composer.vue";
import Tweet from "../components/Tweet.vue";
import { onMounted, ref } from "vue";
import { fetchStream, checkAuth } from "../api/requests";

const loading = ref(true);
const tweets = ref([]);

// Funktion zum Laden des Streams
const loadStream = async () => {
  loading.value = true;
  try {
    const stream = await fetchStream();
    tweets.value = stream;
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
};

// Authentifizierung und Stream laden bei Initialisierung
onMounted(async () => {
  loading.value = true;

  try {
    const response = await checkAuth();
    console.log("checkAuth Resultat", response);

    await loadStream();
  } catch (error) {
    console.error(error);
  }
});

// Event empfangen und Stream neu laden
const handleNewTweet = () => {
  loadStream();
};
</script>

<template>
  <LoginInfo />

  <!-- Composer-Komponente, bei der der 'posted' Event empfangen wird -->
  <Composer @posted="handleNewTweet" />

  <section class="stream" v-if="!loading">
    <Tweet
      v-for="tweet in tweets"
      :key="tweet.id"
      :user="{ id: tweet.user.id, name: tweet.user.name }"
      :text="tweet.text"
      :createdAt="tweet.created_at"
      :likes="tweet.likes || 0"
      :id="tweet.id"
      :liked_tweets="tweet.liked_tweets"
    />
  </section>

  <div class="loading" v-if="loading">Lade Tweets...</div>
</template>
