<script setup>
import { ref } from 'vue'
const props = defineProps({
  username: {type: String, required: true},
  titleClassName: {type: String}
})

const user = ref();

fetch(`https://api.github.com/users/${props.username}`).then(async (res)=>{
  const data = await res.json()
  user.value = data
})
</script>
<template>
  <div v-if="user" class="movie-notification">
  <img :src="user.avatar_url" alt="user-foto" class="movie-poster">
  <div class="notification-content">
    <h2 class="movie-title" :class="props.titleClassName">{{ user.name }}</h2>
    <p class="movie-description">
      <strong>Followers:</strong>{{ user.followers }}
      <strong>Following:</strong>{{ user.following }}
    </p>
    <a :href="user.html_url" class="watch-button">View Profile</a>
  </div>
</div>
</template>
