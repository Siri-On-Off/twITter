<script setup>
import { ref } from "vue"
import { useAuth } from '../api/auth'

const { isLoggedIn } = useAuth()
const tweetText = ref('')
</script>

<template>
  <!-- Composer -->
  <form class="composer" v-if="isLoggedIn">
    <label class="composer__prompt">Was geht?</label>
    <textarea
      maxlength="160"
      class="composer__textarea"
      placeholder="Verfasse einen Tweet..."
      v-model="tweetText"/>
    <div class="composer__actions">
      <div class="composer__stats stats">
        <span class="stats__counter">{{ tweetText.length }}</span>
        <span class="stats__max">/ 160</span>
      </div>
      <button :disabled="tweetText.length < 5" class="btn btn--primary">
        Tweet veröffentlichen
      </button>
    </div>
  </form>
</template>
