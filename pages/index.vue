<template>
  <div class="container mx-auto w-1/2 py-8 divide-y space-y-8 divide-gray-300">
    <PostItem v-for="n in 10" :key="n" />
  </div>
</template>
