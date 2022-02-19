<template>
  <div class="container mx-auto w-1/2 py-8">
    <Title>My Info | {{ title }}</Title>
    <div>
      <div>Name: {{ user?.name }}</div>
      <div>Email: {{ user?.email }}</div>
    </div>

    <div class="mt-4">
      <h3 class="text-2xl">My Posts</h3>
      <ul v-if="posts">
        <li v-for="post in posts" :key="post.id">
          <NuxtLink
            :to="`/posts/${post.id}`"
            class="text-blue-600 hover:underline"
            >{{ post.title }}</NuxtLink
          >
          &middot;
          <NuxtLink
            :to="`/posts/${post.id}/edit`"
            class="text-blue-600 hover:underline"
            >Edit</NuxtLink
          >
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  middleware: ['auth'],
})

const title = useState('title')
const user = ref(null)
const posts = ref([])

const { $apiFetch } = useNuxtApp()

onMounted(async () => {
  user.value = await $apiFetch('/api/user')

  posts.value = await $apiFetch('/api/user/posts')
})
</script>
