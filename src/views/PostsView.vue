<script setup>
import { RouterLink } from "vue-router";
import { storeToRefs } from "pinia";
import {useAuthorStore} from "../stores/author"
import { usePostStore } from "../stores/post";
import Post from "../components/Post.vue"

const route = useRoute()
const {getPostAuthor} = storeToRefs(useAuthorStore())
const {fetchAuthors} = useAuthorStore()
const { posts, loading, error } = storeToRefs(usePostStore());
const { fetchPosts } = usePostStore();

fetchAuthors()
fetchPosts(route.params.id);
</script>

<template>
  <main>
    <p v-if="loading">Loading posts...</p>
    <p v-if="error">{{error.message}}</p>
    <p v-if="post">
      <post :post="post" :author-"getAuthor"></post>
    </p>
    // eslint-disable-next-line vue/no-use-v-if-with-v-for
    <p v-if="posts" v-for="post in posts" :key="post.id">
      <RouterLink :to="`/post/${post.id}`">{{post.title}}</RouterLink>
      <p>{{post.body}}</p>
    </p>
  </main>
</template>
