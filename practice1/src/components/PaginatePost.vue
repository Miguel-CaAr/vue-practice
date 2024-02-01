<script setup>
// const emit = defineEmits(["next", "prev"]);
// No es necesario el defineEmits siempre y cuando el v-on(@) con emit incluya el "$" al incio
</script>
<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button @click="$emit('prev')" type="button" class="btn btn-outline-primary">
      Prev
    </button>
    <button @click="$emit('next')" type="button" class="btn btn-outline-primary">
      Next
    </button>
  </div>
</template>

//61: PAGINACION 3
