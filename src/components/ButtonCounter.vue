<script setup>
import { ref } from 'vue';

const counter = ref(0)
const sum = () => {
  counter.value ++
}
</script>

<template>
  <button @click="sum">{{ counter }}</button>
</template>