<template>
  <NuxtLayout name="dashboard">
    <div class="space-y-6 p-8 bg-background min-h-screen">
      <!-- Page Header -->
      <div class="flex justify-between items-center">
        <div>
          <h2 class="text-3xl font-bold tracking-tight">사용자 관리</h2>
          <p class="text-muted-foreground">
            등록된 사용자들을 관리하고 모니터링하세요.
          </p>
        </div>
        <Button>
          <Icon name="users" class="mr-2 h-4 w-4" />
          새 사용자 추가
        </Button>
      </div>
      
      <!-- Filter Section -->
      <Card>
        <CardContent class="pt-6">
          <div class="flex flex-col sm:flex-row gap-4">
            <Input 
              placeholder="이름 또는 이메일로 검색..." 
              class="flex-1"
            />
            <Button variant="outline">
              <Icon name="search" class="mr-2 h-4 w-4" />
              검색
            </Button>
          </div>
        </CardContent>
      </Card>
      
      <!-- Users Table -->
      <Card>
        <CardHeader>
          <CardTitle>전체 사용자 ({{ users.length }}명)</CardTitle>
        </CardHeader>
        <CardContent>
          <Table>
            <TableHeader>
              <TableRow>
                <TableHead>이름</TableHead>
                <TableHead>이메일</TableHead>
                <TableHead>역할</TableHead>
                <TableHead>가입일</TableHead>
                <TableHead>상태</TableHead>
                <TableHead class="text-right">작업</TableHead>
              </TableRow>
            </TableHeader>
            <TableBody>
              <TableRow v-for="user in users" :key="user.id">
                <TableCell class="font-medium">{{ user.name }}</TableCell>
                <TableCell>{{ user.email }}</TableCell>
                <TableCell>
                  <span :class="cn(
                    'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium',
                    user.role === '관리자'
                      ? 'bg-purple-100 text-purple-800'
                      : user.role === '편집자'
                      ? 'bg-blue-100 text-blue-800'
                      : 'bg-gray-100 text-gray-800'
                  )">
                    {{ user.role }}
                  </span>
                </TableCell>
                <TableCell>{{ user.joinDate }}</TableCell>
                <TableCell>
                  <span :class="cn(
                    'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium',
                    user.status === '활성'
                      ? 'bg-green-100 text-green-800'
                      : 'bg-red-100 text-red-800'
                  )">
                    {{ user.status }}
                  </span>
                </TableCell>
                <TableCell class="text-right">
                  <div class="flex justify-end space-x-2">
                    <Button variant="outline" size="sm">편집</Button>
                    <Button variant="outline" size="sm" class="text-red-600 hover:text-red-700">
                      삭제
                    </Button>
                  </div>
                </TableCell>
              </TableRow>
            </TableBody>
          </Table>
        </CardContent>
      </Card>
      
      <!-- User Statistics -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <Card>
          <CardHeader class="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle class="text-sm font-medium">총 사용자</CardTitle>
            <Icon name="users" class="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div class="text-2xl font-bold">{{ users.length }}</div>
            <p class="text-xs text-green-600">+3명 이번 주</p>
          </CardContent>
        </Card>
        
        <Card>
          <CardHeader class="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle class="text-sm font-medium">활성 사용자</CardTitle>
            <Icon name="users-2" class="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div class="text-2xl font-bold">{{ activeUsers }}</div>
            <p class="text-xs text-green-600">전체의 {{ ((activeUsers / users.length) * 100).toFixed(1) }}%</p>
          </CardContent>
        </Card>
        
        <Card>
          <CardHeader class="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle class="text-sm font-medium">관리자</CardTitle>
            <Icon name="user" class="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div class="text-2xl font-bold">{{ adminUsers }}</div>
            <p class="text-xs text-muted-foreground">시스템 관리자</p>
          </CardContent>
        </Card>
      </div>
    </div>
  </NuxtLayout>
</template>

<script setup lang="ts">
import { cn } from '~/lib/utils'

// SEO
useHead({
  title: '사용자 관리 - Shashboard'
})

// Sample data
const users = [
  {
    id: 1,
    name: '김철수',
    email: 'kim@example.com',
    role: '관리자',
    joinDate: '2024-01-15',
    status: '활성'
  },
  {
    id: 2,
    name: '박영희',
    email: 'park@example.com',
    role: '편집자',
    joinDate: '2024-02-03',
    status: '활성'
  },
  {
    id: 3,
    name: '이민수',
    email: 'lee@example.com',
    role: '사용자',
    joinDate: '2024-02-20',
    status: '비활성'
  },
  {
    id: 4,
    name: '정수진',
    email: 'jung@example.com',
    role: '편집자',
    joinDate: '2024-03-01',
    status: '활성'
  },
  {
    id: 5,
    name: '최영수',
    email: 'choi@example.com',
    role: '사용자',
    joinDate: '2024-03-10',
    status: '활성'
  },
  {
    id: 6,
    name: '한지연',
    email: 'han@example.com',
    role: '사용자',
    joinDate: '2024-03-15',
    status: '활성'
  }
]

const activeUsers = computed(() => {
  return users.filter(user => user.status === '활성').length
})

const adminUsers = computed(() => {
  return users.filter(user => user.role === '관리자').length
})
</script>
