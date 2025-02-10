<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>

<script setup>
import 'aos/dist/aos.css'
import { useHead } from "#imports";

useHead({
  title: "My Portfolio",
  htmlAttrs: {
    lang: "en",
  },
  meta: [
    { name: "description", content: "Welcome to my portfolio site built with Nuxt 3!" },
    { name: "keywords", content: "Nuxt 3, Vue, Portfolio, Software Developer" },
    { property: "og:title", content: "My Portfolio" },
    { property: "og:description", content: "Check out my work and projects." },
    { property: "og:url", content: "https://my-portfolio-kappa-beige-67.vercel.app/" },
    { property: "og:image", content: "https://i.ibb.co/Swk3rtTT/Abhay.webp" },
  ],
});
</script>
<style>
@import url('https://cdnjs.cloudflare.com/ajax/libs/remixicon/3.3.0/remixicon.css');
</style>