<script setup>

const emit = defineEmits(['handleChangeBtnNext', 'handleChangeBtnPrev'])

//activar emit desde otra funcion
const activar = () => {
  emit('handleChangeBtnNext')
}

defineProps(['start', 'maxLength', 'end'])

</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button 
        :disabled="start === 0" 
        type="button" 
        class="btn btn-outline-primary" 
        @click="emit('handleChangeBtnPrev')"
    >Left</button>

    <button 
        :disabled="end === maxLength" 
        type="button" 
        class="btn btn-outline-primary" 
        @click="activar"
    >Right</button>
  </div>
</template>