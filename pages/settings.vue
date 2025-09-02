<template>
  <NuxtLayout name="dashboard">
    <div class="space-y-6">
      <!-- Page Header -->
      <div>
        <h2 class="text-3xl font-bold tracking-tight">설정</h2>
        <p class="text-muted-foreground">
          시스템 설정을 관리하고 개인화 옵션을 조정하세요.
        </p>
      </div>
      
      <!-- Settings Sections -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <!-- Left Sidebar - Settings Menu -->
        <div class="lg:col-span-1">
          <Card>
            <CardHeader>
              <CardTitle class="text-lg">설정 메뉴</CardTitle>
            </CardHeader>
            <CardContent class="p-0">
              <nav class="space-y-1">
                <button
                  v-for="section in settingSections"
                  :key="section.id"
                  :class="cn(
                    'w-full flex items-center px-4 py-3 text-left text-sm transition-colors hover:bg-muted',
                    activeSection === section.id ? 'bg-muted font-medium' : ''
                  )"
                  @click="activeSection = section.id"
                >
                  <Icon :name="section.icon" class="mr-3 h-4 w-4" />
                  {{ section.name }}
                </button>
              </nav>
            </CardContent>
          </Card>
        </div>
        
        <!-- Right Content - Settings Forms -->
        <div class="lg:col-span-2 space-y-6">
          <!-- General Settings -->
          <Card v-if="activeSection === 'general'">
            <CardHeader>
              <CardTitle>일반 설정</CardTitle>
            </CardHeader>
            <CardContent class="space-y-4">
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div class="space-y-2">
                  <label class="text-sm font-medium">사이트 이름</label>
                  <Input value="Shashboard" />
                </div>
                <div class="space-y-2">
                  <label class="text-sm font-medium">관리자 이메일</label>
                  <Input value="admin@example.com" />
                </div>
              </div>
              <div class="space-y-2">
                <label class="text-sm font-medium">사이트 설명</label>
                <Input value="현대적인 대시보드 템플릿" />
              </div>
              <div class="pt-4">
                <Button>변경사항 저장</Button>
              </div>
            </CardContent>
          </Card>
          
          <!-- Security Settings -->
          <Card v-if="activeSection === 'security'">
            <CardHeader>
              <CardTitle>보안 설정</CardTitle>
            </CardHeader>
            <CardContent class="space-y-4">
              <div class="flex items-center justify-between">
                <div class="space-y-0.5">
                  <div class="text-sm font-medium">2단계 인증</div>
                  <div class="text-sm text-muted-foreground">
                    계정 보안을 강화하기 위해 2단계 인증을 활성화하세요.
                  </div>
                </div>
                <Button variant="outline">설정</Button>
              </div>
              
              <div class="flex items-center justify-between">
                <div class="space-y-0.5">
                  <div class="text-sm font-medium">로그인 알림</div>
                  <div class="text-sm text-muted-foreground">
                    새로운 기기에서 로그인 시 이메일 알림을 받습니다.
                  </div>
                </div>
                <Button variant="outline">활성화됨</Button>
              </div>
              
              <div class="space-y-2">
                <label class="text-sm font-medium">비밀번호 변경</label>
                <div class="space-y-2">
                  <Input type="password" placeholder="현재 비밀번호" />
                  <Input type="password" placeholder="새 비밀번호" />
                  <Input type="password" placeholder="새 비밀번호 확인" />
                </div>
                <Button class="w-full">비밀번호 변경</Button>
              </div>
            </CardContent>
          </Card>
          
          <!-- Notification Settings -->
          <Card v-if="activeSection === 'notifications'">
            <CardHeader>
              <CardTitle>알림 설정</CardTitle>
            </CardHeader>
            <CardContent class="space-y-4">
              <div v-for="notification in notificationSettings" :key="notification.id" class="flex items-center justify-between">
                <div class="space-y-0.5">
                  <div class="text-sm font-medium">{{ notification.title }}</div>
                  <div class="text-sm text-muted-foreground">
                    {{ notification.description }}
                  </div>
                </div>
                <Button 
                  :variant="notification.enabled ? 'default' : 'outline'"
                  size="sm"
                  @click="notification.enabled = !notification.enabled"
                >
                  {{ notification.enabled ? '활성화됨' : '비활성화됨' }}
                </Button>
              </div>
              <div class="pt-4">
                <Button>알림 설정 저장</Button>
              </div>
            </CardContent>
          </Card>
          
          <!-- System Settings -->
          <Card v-if="activeSection === 'system'">
            <CardHeader>
              <CardTitle>시스템 설정</CardTitle>
            </CardHeader>
            <CardContent class="space-y-4">
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div class="space-y-2">
                  <label class="text-sm font-medium">언어</label>
                  <select class="w-full h-10 px-3 py-2 text-sm bg-background border border-input rounded-md">
                    <option>한국어</option>
                    <option>English</option>
                    <option>日本語</option>
                  </select>
                </div>
                <div class="space-y-2">
                  <label class="text-sm font-medium">시간대</label>
                  <select class="w-full h-10 px-3 py-2 text-sm bg-background border border-input rounded-md">
                    <option>Asia/Seoul</option>
                    <option>UTC</option>
                    <option>America/New_York</option>
                  </select>
                </div>
              </div>
              
              <div class="space-y-2">
                <label class="text-sm font-medium">테마</label>
                <div class="flex space-x-2">
                  <Button variant="outline" size="sm">라이트</Button>
                  <Button variant="outline" size="sm">다크</Button>
                  <Button variant="outline" size="sm">시스템</Button>
                </div>
              </div>
              
              <div class="pt-4 space-y-2">
                <Button class="w-full">시스템 설정 저장</Button>
                <Button variant="destructive" class="w-full">
                  시스템 재시작
                </Button>
              </div>
            </CardContent>
          </Card>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script setup lang="ts">
import { cn } from '~/lib/utils'

// SEO
useHead({
  title: '설정 - Shashboard'
})

const activeSection = ref('general')

const settingSections = [
  { id: 'general', name: '일반', icon: 'settings' },
  { id: 'security', name: '보안', icon: 'user' },
  { id: 'notifications', name: '알림', icon: 'bell' },
  { id: 'system', name: '시스템', icon: 'settings' }
]

const notificationSettings = ref([
  {
    id: 1,
    title: '새 사용자 가입',
    description: '새로운 사용자가 가입했을 때 알림을 받습니다.',
    enabled: true
  },
  {
    id: 2,
    title: '시스템 업데이트',
    description: '시스템 업데이트가 있을 때 알림을 받습니다.',
    enabled: true
  },
  {
    id: 3,
    title: '보안 경고',
    description: '보안 관련 이벤트 발생 시 알림을 받습니다.',
    enabled: true
  },
  {
    id: 4,
    title: '성능 알림',
    description: '시스템 성능 이슈 발생 시 알림을 받습니다.',
    enabled: false
  }
])
</script>
