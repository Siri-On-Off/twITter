<script setup>
import Widget from "./Widget.vue";
import { onMounted, ref } from "vue";
import { fetchTopUsers } from "../api/requests";

const topUsers = ref([]);
const loading = ref(true);

onMounted(async () => {
  try {
    loading.value = true;

    topUsers.value = await fetchTopUsers();
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
});
</script>

<template>
  <Widget title="Top User">
    <div v-if="loading" class="loading">Lade Top User ...</div>
    <ul v-else class="content-list">
      <li class="content-list__item" v-for="user in topUsers" :key="user.id">
        <a href="#">
          <span class="content-list__meta">{{ user.tweetCount }} Tweets</span>
          <span class="content-list__text">{{ user.name }}</span>
        </a>
      </li>
    </ul>
  </Widget>
</template>
