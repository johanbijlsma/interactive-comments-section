<template>
  <div class="comment">
    <div class="inner-wrapper">
      <div class="vote-buttons">buttons</div>
      <div class="meta">
        <div class="user">
          <img :src="user.image.webp" alt="" />
          <p class="user-name">{{ user.username }}</p>
          <p class="created-at">{{ createdAt }}</p>
        </div>
      </div>
      <div class="main">
        {{ content }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  content: string
  createdAt: string
  user: {
    image: {
      webp: string
      png: string
    }
    username: string
  }
  score: number
}>()
</script>

<style scoped>
.comment {
  background-color: var(--neutral-white);
  border-radius: 10px;
  color: var(--neutral-dark-blue);
  padding: 16px;
  margin-block-end: 16px;
  box-shadow:
    0 0 10px rgba(0, 0, 0, 0.1),
    0 4px 4px rgba(0, 0, 0, 0.1);
}
.inner-wrapper {
  width: 100%;
  display: grid;
  grid-template-areas:
    'vote meta'
    'vote main';
  grid-template-columns: 80px 1fr;
  gap: 8px;
  & .vote-buttons {
    grid-area: vote;
  }
  & .main {
    grid-area: main;
    color: var(--neutral-grayish-blue);
  }
  & .meta {
    grid-area: meta;
    display: flex;
    justify-content: space-between;
    & .user {
      display: flex;
      justify-content: flex-start;
      gap: 16px;
      & img {
        aspect-ratio: 1/1;
        width: 30px;
      }
      & p.user-name {
        font-weight: 700;
      }
      & p.created-at {
        font-weight: 300;
        color: var(--neutral-grayish-blue);
      }
    }
  }
}
</style>
