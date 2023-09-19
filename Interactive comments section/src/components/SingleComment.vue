<template>
  <div class="comment">
    <div class="inner-wrapper">
      <div class="vote-buttons">
        <button @click="increaseVote()">
          <img src="./../components/images/icon-plus.svg" alt="Vote up" srcset="" /></button
        ><Transition name="update"
          ><span class="vote-score" v-if="CommentScore">{{ CommentScore }} </span>
        </Transition>
        <button @click="decreaseVote">
          <img src="./../components/images/icon-minus.svg" alt="Vote down" srcset="" />
        </button>
      </div>
      <div class="meta">
        <div class="user">
          <img :src="user.image.webp" :alt="user.username" />
          <p class="user-name">
            {{ user.username }}
            <template v-if="user.username === commentsData.currentUser.username">
              <span class="username-you-tag"
                >{{ user.username === commentsData.currentUser.username ? 'you' : '' }}
              </span>
            </template>
          </p>

          <p class="created-at">{{ createdAt }}</p>
        </div>
        <button @click="increaseVote()" class="reply">
          <img src="./../components/images/icon-reply.svg" alt="Reply" srcset="" /> Reply
        </button>
      </div>
      <div class="main">
        <span v-if="replyingTo" class="replying-to">@{{ replyingTo }}</span>
        {{ content }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import commentsData from './../data.json'

const props = defineProps<{
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
  replyingTo?: string
}>()

const CommentScore = ref(props.score)

const increaseVote = () => {
  CommentScore.value += 1
}
const decreaseVote = () => {
  CommentScore.value -= 1
}
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
  gap: 8px;

  & .vote-buttons {
    grid-area: vote;
    display: flex;
    flex-direction: column;
    background-color: var(--neutral-light-gray);
    text-align: center;
    border-radius: 10px;
    justify-content: space-between;
    width: 50px;
    margin: 0 auto;
    & button {
      border-color: transparent;
      border-width: 0px;
      background-color: transparent;
      cursor: pointer;
      box-shadow: none;
      /* overflow: hidden; */
      margin: 2px auto;
      display: block;
      flex-grow: 1;
      &:hover img {
        animation: button-hover 800ms 100ms ease-in-out alternate infinite;
      }
    }
    & span {
      color: var(--primary-moderate-blue);
      font-weight: 700;
    }
  }
  & .main {
    grid-area: main;
    color: var(--neutral-grayish-blue);
    & .replying-to {
      color: var(--primary-moderate-blue);
      font-weight: 500;
    }
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
    & span.username-you-tag {
      color: var(--neutral-white);
      background-color: var(--primary-moderate-blue);
      padding: 2px 5px;
      font-size: 80%;
      border-radius: 3px;
    }
  }
  .update-enter-active {
    animation: update 500ms;
  }
  .update-leave-active {
    animation: update 500ms reverse;
  }
}

button.reply {
  background-color: transparent;
  box-shadow: none;
  border: none;
  color: var(--primary-moderate-blue);
  font-weight: 500;
}
.inner-wrapper {
  @media screen and (max-width: 500px) {
    grid-template-areas:
      'meta'
      'main'
      'vote';
    grid-template-columns: auto;
    & .vote-buttons {
      grid-area: vote;
      display: flex;
      flex-direction: row;
      background-color: var(--neutral-light-gray);
      border-radius: 10px;
      justify-content: space-between;
      width: 85px;
      margin: 4px 0;
      & button {
        border-color: transparent;
        border-width: 0px;
        background-color: transparent;
        cursor: pointer;
        box-shadow: none;
        /* overflow: hidden; */
        margin: 4px 0;
        display: block;
        flex-grow: 1;
        &:hover img {
          animation: button-hover 800ms 100ms ease-in-out alternate infinite;
        }
      }
      & span {
        color: var(--primary-moderate-blue);
        font-weight: 700;
      }
    }
  }
  @media screen and (min-width: 500px) {
    grid-template-areas:
      'vote meta'
      'vote main';
    grid-template-columns: 80px 1fr;
  }
}
@keyframes button-hover {
  0% {
    scale: 1;
    backdrop-filter: blur(0px);
  }
  50% {
    scale: 1.5;
    backdrop-filter: blur(1px);
    filter: hue-rotate(180deg);
  }
  100% {
    scale: 1;
    backdrop-filter: blur(0px);
    filter: hue-rotate(0deg);
  }
}
@keyframes update {
  0% {
    scale: 0.45;
    opacity: 0;
  }
  40% {
    scale: 1.12;
  }
  100% {
    scale: 1;
    opacity: 1;
  }
}
</style>
