<script setup>
import { computed, onMounted, ref } from 'vue';

import BlogPost from './components/BlogPost.vue';
import ButtonPagination from './components/ButtonPagination.vue';
import Spinner from './components/Spinner.vue'


const posts = ref([])
const favorite = ref('')
const start = ref(0)
const end = ref(10)
const loading = ref(true)

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then((res)=> res.json())
//   .then((data)=> posts.value = data)
//   .catch(e => console.log(e))
//   .finally(() => loading.value = false)

// onMounted(async () => {
//   try {
//     const res = await fetch('https://jsonplaceholder.typicode.com/posts')
//     posts.value = await res.json()
//   } catch (error) {
//     console.log(error);
//   } finally {
//     loading.value = false
//   }
// })

const fetchData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false
  }
}

fetchData()


const changeFavoritePost = (title) => {
  favorite.value = title
}

//buttons
const handleChangeBtnNext = () => {
  end.value = end.value + 10
  start.value = start.value + 10

  // if(end.value >= posts.value.length){
  //   end.value = 10
  //   start.value = 0
  // } else {
  //   end.value = end.value + 10
  //   start.value = start.value + 10
  // }
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
    <h1>POSTS</h1>
    <p>Favorito: {{ favorite ? favorite : 'Clickea un post favorito' }}</p>
    <Spinner v-if="loading" />

    <div v-else>
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
  </div>
</template>