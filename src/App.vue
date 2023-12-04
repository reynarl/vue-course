<script setup>
import { ref } from 'vue';

import BlogPost from './components/BlogPost.vue';


const posts = ref([])

fetch('https://jsonplaceholder.typicode.com/posts')
.then((res)=> res.json())
.then((data)=> posts.value = data)

const favorite = ref('')

const changeFavoritePost = (title) => {
  favorite.value = title
}

</script>

<template>
  <div class="container">
    <h1>APP</h1>
    <p>Favorito: {{ favorite ? favorite : 'Clickea un post favorito' }}</p>
  <BlogPost 
  v-for="post in posts"
    :id=post.id
    :title=post.title
    :body=post.body
    :colorText=post.colorText
    @changeFavoritePost = changeFavoritePost
  >
</BlogPost>
  </div>
</template>