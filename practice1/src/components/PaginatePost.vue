<script setup>
defineProps(["inicio", "fin", "maxLength"]);
// const emit = defineEmits(["next", "prev"]);
// No es necesario el defineEmits siempre y cuando el v-on(@) con emit incluya el "$" al incio
</script>
<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      @click="$emit('prev')"
      type="button"
      class="btn btn-outline-primary"
      :disabled="inicio <= 0"
    >
      Prev
    </button>
    <button
      @click="$emit('next')"
      type="button"
      class="btn btn-outline-primary"
      :disabled="fin >= maxLength"
    >
      Next
    </button>
  </div>
</template>

//61: PAGINACION 3
