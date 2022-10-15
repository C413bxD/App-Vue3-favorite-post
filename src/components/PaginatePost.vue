<script setup>
defineProps(["start", "end", "maxLength"]);
const emit = defineEmits(["prev", "next"]);
</script>
<template>

  <div class="text-center">
      <div class="btn-group" role="group" aria-label="Basic example">
        <button
          type="button"
          @click="emit('prev')"
          class="btn btn-outline-primary"
          :disabled="start <= 0"
        >
          Previus {{ start }}
        </button>
        <button
          type="button"
          @click="emit('next')"
          class="btn btn-outline-primary"
          :disabled="end >= maxLength"
        >
          Next {{ end }}
        </button>
      </div>
  </div>
</template>
