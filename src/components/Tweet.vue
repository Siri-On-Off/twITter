<script setup>
import { format, formatDistance } from "date-fns";
import { de } from "date-fns/locale";
import { likeTweet } from "../api/requests";
import { ref } from "vue";
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
});

//Day.Month.Year HH:MM
//const formattedDate = format(new Date(props.createdAt), "dd.MM.yyyy HH:mm");
const distance = formatDistance(new Date(props.createdAt), new Date(), {
  locale: de,
});

const currentLikes = ref(props.likes);

const addLikes = async () => {
  if (!isLoggedIn.value) {
    return;
  }

  try {
    const tweet = await likeTweet(props.id);
    currentLikes.value = tweet.likes;
  } catch (error) {
    console.error(error);
  }
};
</script>

<template>
  <div class="tweet">
    <div class="tweet__avatar">
      <img :src="`https://i.pravatar.cc/100?u=${user.id}`" alt="" />
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
        <button @click.prevent="addLikes" v-if="isLoggedIn">
          {{ currentLikes }} 💗
        </button>
        <RouterLink to="/login" v-else>
          {{ currentLikes }} 💗
        </RouterLink>
      </div>
    </div>
  </div>
</template>
