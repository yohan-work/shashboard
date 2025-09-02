<template>
  <div class="min-h-screen flex items-center justify-center bg-background">
    <div class="text-center">
      <Icon name="layout-dashboard" class="h-16 w-16 mx-auto mb-4 text-primary" />
      <h1 class="text-2xl font-bold mb-2">Shashboard로 이동 중...</h1>
      <p class="text-muted-foreground">잠시만 기다려주세요.</p>
    </div>
  </div>
</template>

<script setup lang="ts">
// Redirect to dashboard
await navigateTo('/dashboard')
</script>
