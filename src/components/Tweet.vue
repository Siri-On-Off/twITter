<script setup>
import { formatDistance } from "date-fns";
import { de } from "date-fns/locale";
import { likeTweet } from "../api/requests";
import { ref, computed } from "vue";
import { useAuth } from "../api/auth";
import { RouterLink } from "vue-router";

const { isLoggedIn } = useAuth();

const props = defineProps({
  likes: {
    type: Number,
    required: true,
    default: 0,
  },
  user: {
    type: Object,
    required: true,
  },
  text: {
    type: String,
    required: true,
  },
  createdAt: {
    type: String,
    required: true,
  },
  id: {
    type: Number,
    required: true,
  },
  liked_tweets: {
    type: Array,
    required: true,
    default: () => [],
  },
});

const distance = formatDistance(new Date(props.createdAt), new Date(), {
  locale: de,
});

const currentLikes = ref(props.likes);
const alreadyLiked = computed(() => props.liked_tweets.includes(props.id));
const errorMessage = ref("");

const addLikes = async () => {
  if ( !isLoggedIn || alreadyLiked.value ) {
    return;
  }

  try {
    const tweet = await likeTweet(props.id);
    currentLikes.value = tweet.likes;
  } catch (error) {
    console.error(error);
    errorMessage.value = "Failed to like the tweet. Please try again.";
  }
};
</script>

<template>
  <div class="tweet">
    <div class="tweet__avatar">
      <img :src="`https://i.pravatar.cc/100?u=${user.id}`" alt="User avatar" />
    </div>
    <div class="tweet__content">
      <div class="tweet__header">
        <span class="tweet__author">{{ user.name }}</span>
        <span class="tweet__timestamp">{{ distance }}</span>
      </div>
      <div class="tweet__text">
        {{ text }}
      </div>
      <div class="tweet__likes">
        <button @click.prevent="addLikes" 
        :disabled="!isLoggedIn || alreadyLiked"
        >
          {{ currentLikes }} 💗
        </button>
        <RouterLink to="/login" v-if="!isLoggedIn"> 
          Login to like 
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<style scoped>
.error {
  color: red;
  font-size: 0.9em;
}
</style>