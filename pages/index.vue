<template>
  <div class="container mx-auto w-1/2 py-8 divide-y space-y-8 divide-gray-300">
    <PostItem v-for="post in posts" :key="post.id" :post="post" />
  </div>
</template>

<script setup>
// const nuxtApp = useNuxtApp()
// const { data: posts } = await useFetch('/api/posts', {
//   baseURL: 'http://localhost:8000',
// })
const posts = await useNuxtApp().$apiFetch('/api/posts')
</script>
