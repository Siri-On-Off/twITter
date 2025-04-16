<script setup>
import { ref } from "vue"
import { useAuth } from '../api/auth'
import { createTweet } from './../api/requests'

const { isLoggedIn } = useAuth()
const tweetText = ref('')

function sendTweet() {
  console.log("Tweet senden:", tweetText.value)
  createTweet(tweetText.value)
  tweetText.value = ''
}
</script>


<template>
  <!-- Composer -->
  <form class="composer" v-if="isLoggedIn" @submit.prevent="sendTweet">
    <label class="composer__prompt">Was geht?</label>
    <textarea
      maxlength="160"
      class="composer__textarea"
      placeholder="Verfasse einen Tweet..."
      v-model="tweetText" />
    <div class="composer__actions">
      <div class="composer__stats stats">
        <span class="stats__counter">{{ tweetText.length }}</span>
        <span class="stats__max">/ 160</span>
      </div>
      <span @submit.prevent="handleSubmit">
        <button class="btn btn--primary" type="submit" :disabled="tweetText.length < 5">
          Tweet veröffentlichen
        </button>
      </span>
    </div>
  </form>
</template>
