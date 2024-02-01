<script setup>
import { ref } from "vue";

import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";

const posts = ref([]);
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);

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

fetch("https://jsonplaceholder.typicode.com/posts")
  .then((res) => res.json())
  .then((data) => (posts.value = data));
</script>

<template>
  <header>
    <div>
      <h1>APP</h1>
      <h2>Mi post favorito: {{ favorito }}</h2>
    </div>
  </header>

  <main>
    <PaginatePost @next="next" @prev="prev" class="my-3" />

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

<style scoped></style>
