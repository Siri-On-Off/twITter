<script setup>
import { format, formatDistance } from "date-fns";
import { de } from 'date-fns/locale';

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

const formattedDate = format(new Date(props.createdAt), "dd.MM.yyyy HH:mm");
const distance = formatDistance(
  new Date(props.createdAt), 
  new Date(),
  {locale: de}
)

console.log(distance)
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
    </div>
  </div>
</template>
