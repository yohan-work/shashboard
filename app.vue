<template>
  <Html class="dark">
    <Body class="min-h-screen bg-background font-sans antialiased">
      <NuxtPage />
    </Body>
  </Html>
</template>

<script setup>
// Enable SSR
useHead({
  title: "Shashboard - Dashboard Template",
  meta: [
    {
      name: "description",
      content: "A modern dashboard built with Nuxt 3 and shadcn-vue",
    },
  ],
});
</script>
