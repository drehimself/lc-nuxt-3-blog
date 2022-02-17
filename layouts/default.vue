<template>
  <div class="bg-gray-100 min-h-screen text-gray-900">
    <Title>{{ title }}</Title>
    <nav class="bg-white shadow text-lg px-6 py-6">
      <div class="container mx-auto flex items-center justify-between px-6">
        <div>
          <NuxtLink to="/">Logo</NuxtLink>
        </div>
        <div>
          <ul class="flex space-x-12">
            <li><NuxtLink to="/">Home</NuxtLink></li>
            <li><NuxtLink to="/login">Login</NuxtLink></li>
            <li><NuxtLink to="/register">Register</NuxtLink></li>
            <li><NuxtLink to="/my-info">My Info</NuxtLink></li>
            <li><NuxtLink to="/create">Create</NuxtLink></li>
            <li><NuxtLink to="/about">About</NuxtLink></li>
            <li><NuxtLink to="/contact">Contact</NuxtLink></li>
            <li><a href="#" @click.prevent="logout">Logout</a></li>
          </ul>
        </div>
      </div>
    </nav>
    <slot />
  </div>
</template>

<script setup>
const title = useState('title', () => 'Nuxt 3 Blog')
const { $apiFetch } = useNuxtApp()

async function logout() {
  try {
    await $apiFetch('/logout', {
      method: 'POST',
    })
  } catch (err) {
    console.log(err.data)
  } finally {
    window.location.pathname = '/'
  }
}
</script>

<style>
.router-link-active {
  font-weight: bold;
}
</style>
