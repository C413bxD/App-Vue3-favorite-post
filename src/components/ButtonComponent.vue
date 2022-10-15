<script setup>
import { ref } from "vue";

const counter = ref(0)
const increment = ()=>counter.value++
</script>
<template>
  <button v-on:click="increment"> Counter {{counter}}</button>
</template>