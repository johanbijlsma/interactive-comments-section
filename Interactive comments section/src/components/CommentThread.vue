<script setup lang="ts">
import SingleComment from './SingleComment.vue'
import commentsData from './../data.json'
defineProps<{
  msg: string
}>()
</script>

<template>
  <div class="greetings">
    <!-- now loop over the comments from data.json and pipe them into SingleComment -->
    <div v-for="comment in commentsData.comments" :key="comment.id">
      <SingleComment
        :content="comment.content"
        :createdAt="comment.createdAt"
        :score="comment.score"
        :user="comment.user"
      />
    </div>
    <div class="card">
      <img :src="commentsData.currentUser.image.png" alt="" />
      <p>{{ commentsData.currentUser.username }}</p>
      <pre>{{ commentsData }}</pre>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
