<script setup>
import { ref, computed, onMounted } from "vue";

import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([]);
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const favorito = ref("");

const cambiarFavorito = (title) => {
  favorito.value = title;
};

const next = () => {
  inicio.value += +postXpage;
  fin.value += +postXpage;
};

const prev = () => {
  inicio.value += -postXpage;
  fin.value += -postXpage;
};

onMounted(async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false;
  }
});

// fetch("https://jsonplaceholder.typicode.com/posts")
//   .then((res) => res.json())
//   .then((data) => {
//     posts.value = data;
//   })
//   .finally(() => {
//     loading.value = false;
//   });

const maxLength = computed(() => {
  return posts.value.length;
});
</script>

<template>
  <LoadingSpinner v-if="loading" />
  <template v-else>
    <header>
      <div>
        <h1>APP</h1>
        <h2>Mi post favorito: {{ favorito }}</h2>
      </div>
    </header>
    <main>
      <PaginatePost
        @next="next"
        @prev="prev"
        class="my-3"
        :inicio="inicio"
        :fin="fin"
        :maxLength="maxLength"
      />

      <BlogPost
        v-for="post in posts.slice(inicio, fin)"
        :key="post.id"
        :title="post.title"
        :id="post.id"
        :body="post.body"
        :cambiarFavorito="cambiarFavorito"
      ></BlogPost>
    </main>
  </template>
</template>

<style scoped></style>
