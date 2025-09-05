<script setup>
import { faker } from '@faker-js/faker'
import {computed, ref} from 'vue'
import Post from './components/Post.vue'

const posts = ref([
  { id: 1, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 8 },
  { id: 2, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 0 },
  { id: 3, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: -4 },
  { id: 4, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 0 },
  { id: 5, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: -8 },
  { id: 6, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 4 },
  { id: 7, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 6 },
  { id: 8, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 3 },
  { id: 9, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 15 },
])

function voteUp (id) {
  console.log('voteUp', id)
  const post = posts.value.find(post => post.id === id)
  if (post) post.votes++
}

function voteDown (id) {
  console.log('voteDown', id)
  const post = posts.value.find(post => post.id === id)
  if(post) post.votes--
}

let sortedList = computed(() => {
  return [...posts.value].sort((a, b) => b.votes - a.votes)
})

</script>

<template>
  <div class="container" v-for="post in sortedList">
    <Post :key="post.id" :title="post.title" :text="post.text" :user="post.user" :votes="post.votes" @vote-up="voteUp(post.id)" @vote-down="voteDown(post.id)"></Post>
  </div>
</template>

<style>
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
  font-size: 16px;
  background: #f0f0f0;
}

.container {
  max-width: 800px;
  margin: 40px auto;
  border: 1px solid #fafafa;
  box-shadow: 0 0 2px rgba(0, 0, 0, .2);
  background: #fff;
  border-radius: 4px;
  position: relative;
}
</style>