<script setup lang="ts">
useHead({
  meta: [
    { charset: 'utf-8' },
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [{ rel: 'icon', href: '/favicon.svg' }],
  htmlAttrs: {
    lang: 'en'
  },
  bodyAttrs: {
    style: 'background-color: #000212'
  }
});

useSeoMeta({
  titleTemplate: 'Linear Card - Nuxt'
});
</script>

<template>
  <div>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>
