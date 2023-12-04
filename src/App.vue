<script setup>
import { computed, ref } from 'vue';

import BlogPost from './components/BlogPost.vue';
import ButtonPagination from './components/ButtonPagination.vue';


const posts = ref([])
const favorite = ref('')
const start = ref(0)
const end = ref(10)

fetch('https://jsonplaceholder.typicode.com/posts')
.then((res)=> res.json())
.then((data)=> posts.value = data)


const changeFavoritePost = (title) => {
  favorite.value = title
}

//buttons
const handleChangeBtnNext = () => {
  // if(end.value >= posts.value.length){
  //   end.value = 10
  //   start.value = 0
  // } else {
  //   end.value = end.value + 10
  //   start.value = start.value + 10
  // }

  end.value = end.value + 10
  start.value = start.value + 10
}

const handleChangeBtnPrev = () => {
  end.value = end.value - 10
  start.value = start.value - 10
}

//usamos computed para estar a la escucha de si existen cambios de la longitud de los posts
const maxLength = computed(() => posts.value.length)

</script>

<template>
  <div class="container">
    <h1>APP</h1>
    <p>Favorito: {{ favorite ? favorite : 'Clickea un post favorito' }}</p>
    <ButtonPagination 
      class="mb-3"
      :start="start"
      :end="end"
      :maxLength="maxLength"
      @handleChangeBtnNext = "handleChangeBtnNext"
      @handleChangeBtnPrev = "handleChangeBtnPrev"
    />
    <BlogPost 
    v-for="post in posts.slice(start,end)"
      :id="post.id"
      :title="post.title"
      :body="post.body"
      :colorText="post.colorText"
      @changeFavoritePost = "changeFavoritePost"
    >
  </BlogPost>
  </div>
</template>