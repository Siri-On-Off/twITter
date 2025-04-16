<script setup>
import { format, parseISO } from "date-fns";
import { computed } from "vue";

const props = defineProps({
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
});

const formattedDate = computed(() =>
  format(parseISO(props.createdAt), "dd.MM.yyyy HH:mm")
);
</script>

<template>
  <div class="tweet">
    <div class="tweet__avatar">
      <img :src="`https://i.pravatar.cc/100?u=${user.id}`" alt="" />
    </div>
    <div class="tweet__content">
      <div class="tweet__header">
        <span class="tweet__author">{{ user.name }}</span>
        <span class="tweet__timestamp">{{ formattedDate }}</span>
      </div>
      <div class="tweet__text">
        {{ text }}
      </div>
    </div>
  </div>
</template>
