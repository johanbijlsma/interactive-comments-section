<script setup lang="ts">
import CommentThread from './components/CommentThread.vue'
</script>

<template>
  <main>
    <h1>blabla</h1>
    <CommentThread msg="Interactive comments section" />
  </main>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@400;500;700&display=swap');
:root {
  --primary-moderate-blue: hsl(238, 40%, 52%);
  --primary-soft-red: hsl(358, 79%, 66%);
  --primary-light-grayish-blue: hsl(239, 57%, 85%);
  --primary-pale-red: hsl(357, 100%, 86%);
  --neutral-dark-blue: hsl(212, 24%, 26%);
  --neutral-grayish-blue: hsl(211, 10%, 45%);
  --neutral-light-gray: hsl(223, 19%, 93%);
  --neutral-very-light-gray: hsl(228, 33%, 97%);
  --neutral-white: hsl(0, 0%, 100%);
  --mobile-width: 375px;
  --desktop-width: 1440px;
}
body {
  background-color: var(--neutral-very-light-gray);
}
#app {
  font-family: Rubik, Helvetica, Arial, sans-serif;
  font-size: 16px;
}
h1 {
  color: var(--primary-moderate-blue);
}
</style>
