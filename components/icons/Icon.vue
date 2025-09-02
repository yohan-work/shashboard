<template>
  <component :is="iconComponent" v-bind="$attrs" />
</template>

<script setup lang="ts">
import {
  LayoutDashboard,
  Users,
  Settings,
  Search,
  Menu,
  X,
  TrendingUp,
  DollarSign,
  Users2,
  Bell,
  User
} from 'lucide-vue-next'

interface Props {
  name: string
}

const props = defineProps<Props>()

const icons = {
  'layout-dashboard': LayoutDashboard,
  'users': Users,
  'settings': Settings,
  'search': Search,
  'menu': Menu,
  'x': X,
  'trending-up': TrendingUp,
  'dollar-sign': DollarSign,
  'users-2': Users2,
  'bell': Bell,
  'user': User
}

const iconComponent = computed(() => {
  return icons[props.name as keyof typeof icons] || LayoutDashboard
})
</script>
