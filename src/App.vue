<script setup>
import { computed, onMounted, ref } from "vue";
import PaginatePost from "./components/PaginatePost.vue";
import BlogPost from "./components/BlogPost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([
  { title: "Post01", id: 1, body: "descripcion 1" },
  { title: "Post02", id: 2, body: "descripcion 1" },
  { title: "Post03", id: 3, body: "descripcion 1" },
  { title: "Post04", id: 4 },
]);

const favorito = ref("");
const numXpage = 10;
const start = ref(0);
const end = ref(numXpage);
const loading = ref(true);

const cambiarFavorito = (title) => {
  favorito.value = title;
};

const maxLength = computed(() => posts.value.length);

onMounted(async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }
});

// fetch("https://jsonplaceholder.typicode.com/posts")
//   .then((res) => res.json())
//   .then((data) => {
//     posts.value = data;
//   })
//   .catch((error) => console.log(error))
//   .finally(() => {
//     setTimeout(() => {
//       loading.value = false;
//     }, 2000);
//   });

const next = () => {
  if (end.value <= 90) {
    start.value = start.value + numXpage;
    end.value = end.value + numXpage;
  }
};

const prev = () => {
  if (start.value >= 10) {
    start.value = start.value - numXpage;
    end.value = end.value - numXpage;
  }
};
</script>
<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>App</h1>
    <h5>Mi post favorito: {{ favorito }}</h5>

    <PaginatePost
      @next="next"
      @prev="prev"
      :start="start"
      :end="end"
      :maxLength="maxLength"
      class="mb-2"
    />

    <BlogPost
      v-for="post in posts.slice(start, end)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @cambiarFavorito="cambiarFavorito"
      class="mb-2"
    />
  </div>
</template>
