<template>
  <main v-if="showPost" class="md:col-start-2 lg:col-start-3 md:col-end-12 lg:col-end-11 min-h-full">
    <header>
      <h1 class="text-xl text-white p-6 bg-black">{{ post.title }}</h1>
      <span class="block p-6 text-green">{{ user.name }}</span>
    </header>
    <section class="p-6">
      <p>
        {{ post.body }}
      </p>
    </section>
    <footer class="p-6">
      <NuxtLink to="/" class="bg-green hover:bg-black hover:text-white p-2">Overview</NuxtLink>
    </footer>
  </main>
</template>

<script setup>
import { computed } from 'vue';

const route = useRoute();
const { apiFetch } = useApi();
const { id } = route.params
const { data: post } = await apiFetch(`posts/${id}`);
const { data: user } = await apiFetch(`users/${post.value?.userId}`);
const showPost = computed(() => post.value && user.value);
</script>
