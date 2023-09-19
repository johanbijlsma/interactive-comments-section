<script setup lang="ts">
import SingleComment from './SingleComment.vue'
import commentsData from './../data.json'
import { ref } from 'vue'
defineProps<{
  msg: string
}>()

let CommentsLocal: any
let loading = ref(false)

const addCommentstoLocalStorage = () => {
  loading.value = true
  if (!localStorage.getItem('comments')) {
    localStorage.setItem('comments', JSON.stringify(commentsData))
    JSON.parse(localStorage.getItem('comments') as string)
    loading.value = false
  } else {
    loading.value = false
    return (CommentsLocal = JSON.parse(localStorage.getItem('comments') as string))
  }
}

const updateCommentstoLocalStorage = () => {
  if (localStorage.getItem('comments')) {
    localStorage.setItem('comments', JSON.stringify(commentsData))
    JSON.parse(localStorage.getItem('comments') as string)
  } else {
    localStorage.setItem('comments', JSON.stringify(commentsData))
    JSON.parse(localStorage.getItem('comments') as string)
  }
}
const newComment = ref({
  content: '',
  createdAt: new Date().toLocaleDateString(),
  score: 0,
  replyingTo: '',
  user: commentsData.currentUser,
  replies: [],
  id: CommentsLocal ? CommentsLocal.comments.length + 1 : 348
})

const addComment = () => {
  CommentsLocal.comments.push(newComment.value)
  console.log(newComment.value)
  updateCommentstoLocalStorage()
  newComment.value.content = ''
}

addCommentstoLocalStorage()
</script>

<template>
  <div>
    <template v-if="loading">Loading..</template>
    <template v-if="!loading">
      <div v-for="comment in CommentsLocal?.comments" :key="comment.id">
        <SingleComment
          :content="comment.content"
          :createdAt="comment.createdAt"
          :score="comment.score"
          :user="comment.user"
        />
        <div v-if="comment.replies.length" class="reply-wrapper">
          <div v-for="reply in comment.replies" :key="reply.id">
            <SingleComment
              :content="reply.content"
              :createdAt="reply.createdAt"
              :score="reply.score"
              :user="reply.user"
              :replyingTo="reply.replyingTo"
              class="reply"
            />
          </div>
        </div>
      </div>
      <div class="card add-comment">
        <div class="inner-wrapper">
          <img
            :src="commentsData.currentUser.image.webp"
            :alt="commentsData.currentUser.username"
          />
          <textarea
            name="newComment"
            id="newComment"
            cols="30"
            rows="3"
            placeholder="Add a comment..."
            resize="none"
            v-model="newComment.content"
          ></textarea>
          <button class="button" @click="addComment">Send</button>
        </div>
      </div>
    </template>
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

.add-comment {
  background-color: var(--neutral-white);
  border-radius: 10px;
  color: var(--neutral-dark-blue);
  padding: 16px;
  margin-block-end: 16px;
  box-shadow:
    0 0 10px rgba(0, 0, 0, 0.1),
    0 4px 4px rgba(0, 0, 0, 0.1);
  & .inner-wrapper {
    width: 100%;
    display: grid;
    gap: 8px;

    & img {
      aspect-ratio: 1/1;
      width: 40px;
      margin: 0 auto;
    }

    & textarea {
      border-radius: 10px;
      padding: 16px;
      font-family: Rubik, Helvetica, Arial, sans-serif;
      font-size: 16px;
      color: var(--neutral-dark-blue);
      border-color: var(--neutral-light-gray);
    }
    & button.button {
      border-radius: 10px;
      background-color: var(--primary-moderate-blue);
      text-transform: uppercase;
      color: var(--neutral-white);
      font-weight: 700;
      max-height: 50px;
      box-shadow: none;
      border: none;
      &:hover {
        animation: button-hover 800ms 100ms ease-in-out alternate infinite;
      }
    }
  }
}

.reply-wrapper {
  margin-block-end: 16px;
}
.comment.reply {
  margin-inline-start: 64px;
  position: relative;
  &::before {
    content: '';
    background-color: var(--neutral-light-gray);
    display: block;
    width: 0.25rem;
    position: absolute;
    height: 111%;
    translate: -56px -26px;
  }
}

.inner-wrapper {
  @media screen and (max-width: 500px) {
    grid-template-areas:
      'meta'
      'main'
      'vote';
    grid-template-columns: auto;
    & .vote-buttons {
      /* grid-area: vote;
      display: flex;
      flex-direction: row;
      background-color: var(--neutral-light-gray);
      border-radius: 10px;
      justify-content: space-between;
      width: 85px;
      margin: 4px 0; */
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
    grid-template-areas: 'vote meta button';
    grid-template-columns: 80px 1fr 150px;
  }
}
</style>
