<template>
  <div class="min-h-screen flex bg-background">
    <!-- Mobile Sidebar Backdrop -->
    <div 
      v-if="isMobileSidebarOpen" 
      class="fixed inset-0 z-40 bg-black bg-opacity-50 lg:hidden"
      @click="closeMobileSidebar"
    ></div>
    
    <!-- Sidebar -->
    <aside 
      :class="cn(
        'fixed inset-y-0 z-50 w-64 bg-card border-r border-border transition-transform duration-200 ease-in-out lg:translate-x-0 lg:static lg:inset-0',
        isMobileSidebarOpen ? 'translate-x-0' : '-translate-x-full'
      )"
    >
      <div class="flex items-center justify-between h-16 px-6 border-b border-border">
        <h1 class="text-xl font-bold text-foreground">Shashboard</h1>
        <Button 
          variant="ghost" 
          size="icon" 
          class="lg:hidden"
          @click="closeMobileSidebar"
        >
          <Icon name="x" class="h-6 w-6" />
        </Button>
      </div>
      
      <nav class="p-4">
        <ul class="space-y-2">
          <li v-for="item in navigation" :key="item.name">
            <NuxtLink
              :to="item.href"
              :class="cn(
                'flex items-center px-3 py-2 text-sm font-medium rounded-md transition-colors',
                isActiveRoute(item.href)
                  ? 'bg-secondary text-secondary-foreground'
                  : 'text-muted-foreground hover:bg-secondary hover:text-secondary-foreground'
              )"
            >
              <Icon :name="item.icon" class="mr-3 h-5 w-5" />
              {{ item.name }}
            </NuxtLink>
          </li>
        </ul>
      </nav>
    </aside>
    
    <!-- Main Content -->
    <div class="flex-1 flex flex-col">
      <!-- Header -->
      <header class="h-16 bg-card border-b border-border flex items-center justify-between px-4 lg:px-6">
        <div class="flex items-center">
          <Button 
            variant="ghost" 
            size="icon" 
            class="lg:hidden mr-2"
            @click="openMobileSidebar"
          >
            <Icon name="menu" class="h-6 w-6" />
          </Button>
          
          <!-- Search -->
          <div class="relative hidden sm:block">
            <Icon name="search" class="absolute left-3 top-1/2 transform -translate-y-1/2 h-4 w-4 text-muted-foreground" />
            <Input 
              placeholder="검색..." 
              class="pl-9 w-64"
            />
          </div>
        </div>
        
        <div class="flex items-center space-x-4">
          <Button variant="ghost" size="icon">
            <Icon name="bell" class="h-5 w-5" />
          </Button>
          <Button variant="ghost" size="icon">
            <Icon name="user" class="h-5 w-5" />
          </Button>
        </div>
      </header>
      
      <!-- Page Content -->
      <main class="flex-1 p-4 lg:p-6 bg-background">
        <slot />
      </main>
    </div>
  </div>
</template>

<script setup lang="ts">
import { cn } from '~/lib/utils'

const route = useRoute()

const isMobileSidebarOpen = ref(false)

const navigation = [
  { name: '대시보드', href: '/dashboard', icon: 'layout-dashboard' },
  { name: '사용자', href: '/users', icon: 'users' },
  { name: '설정', href: '/settings', icon: 'settings' }
]

const openMobileSidebar = () => {
  isMobileSidebarOpen.value = true
}

const closeMobileSidebar = () => {
  isMobileSidebarOpen.value = false
}

const isActiveRoute = (href: string) => {
  return route.path === href
}

// Close mobile sidebar when route changes
watch(() => route.path, () => {
  isMobileSidebarOpen.value = false
})
</script>
