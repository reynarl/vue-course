<script setup>

//1. props como array
// defineProps(['title', 'body', 'id', 'colorText'])

//2. si queremos usar los props dentro del script podemos acceder a ellos de esta forma:
// const props = defineProps(['title', 'body', 'id', 'colorText'])
// console.log(props.title);

//3. Props como objeto:

defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: 'Sin descripcion',
  },
  colorText: String
})

const emit = defineEmits(['changeFavoritePost'])

</script>

<template>
  <div class="card">
    <div class="card-body">
    <h5 class="card-title" :class="`text-${ colorText }`">{{ id }} - {{title}}</h5>
      <p>{{ body }}</p>
      <button class="btn btn-outline-secondary" @click="emit('changeFavoritePost', title)">
        Favorito
      </button>
    </div>
  </div>
</template>