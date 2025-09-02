<template>
  <div :class="cn('rounded-xl border bg-card text-card-foreground shadow-sm hover:shadow-md transition-shadow duration-200', $attrs.class)">
    <slot />
  </div>
</template>

<script setup lang="ts">
import { cn } from '~/lib/utils'

interface Props {
  class?: string
}

defineProps<Props>()
</script>
