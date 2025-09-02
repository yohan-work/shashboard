<template>
  <thead :class="cn('[&_tr]:border-b', $attrs.class)">
    <slot />
  </thead>
</template>

<script setup lang="ts">
import { cn } from '~/lib/utils'

interface Props {
  class?: string
}

defineProps<Props>()
</script>
