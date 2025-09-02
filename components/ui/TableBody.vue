<template>
  <tbody :class="cn('[&_tr:last-child]:border-0', $attrs.class)">
    <slot />
  </tbody>
</template>

<script setup lang="ts">
import { cn } from '~/lib/utils'

interface Props {
  class?: string
}

defineProps<Props>()
</script>
