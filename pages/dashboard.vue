<template>
  <NuxtLayout name="dashboard">
    <div class="space-y-6">
      <!-- Page Header -->
      <div>
        <h2 class="text-3xl font-bold tracking-tight">대시보드</h2>
        <p class="text-muted-foreground">
          전체적인 비즈니스 현황을 한눈에 확인하세요.
        </p>
      </div>
      
      <!-- Stats Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
        <Card v-for="stat in stats" :key="stat.title">
          <CardHeader class="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle class="text-sm font-medium">{{ stat.title }}</CardTitle>
            <Icon :name="stat.icon" class="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div class="text-2xl font-bold">{{ stat.value }}</div>
            <p :class="cn('text-xs', stat.change > 0 ? 'text-green-600' : 'text-red-600')">
              {{ stat.change > 0 ? '+' : '' }}{{ stat.change }}% 지난 달 대비
            </p>
          </CardContent>
        </Card>
      </div>
      
      <!-- Recent Activity Table -->
      <Card>
        <CardHeader>
          <CardTitle>최근 사용자 활동</CardTitle>
        </CardHeader>
        <CardContent>
          <Table>
            <TableHeader>
              <TableRow>
                <TableHead>사용자</TableHead>
                <TableHead>활동</TableHead>
                <TableHead>시간</TableHead>
                <TableHead>상태</TableHead>
              </TableRow>
            </TableHeader>
            <TableBody>
              <TableRow v-for="activity in recentActivity" :key="activity.id">
                <TableCell class="font-medium">{{ activity.user }}</TableCell>
                <TableCell>{{ activity.action }}</TableCell>
                <TableCell>{{ activity.time }}</TableCell>
                <TableCell>
                  <span :class="cn(
                    'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium',
                    activity.status === '성공' 
                      ? 'bg-green-100 text-green-800' 
                      : 'bg-red-100 text-red-800'
                  )">
                    {{ activity.status }}
                  </span>
                </TableCell>
              </TableRow>
            </TableBody>
          </Table>
        </CardContent>
      </Card>
      
      <!-- Chart Placeholder -->
      <Card>
        <CardHeader>
          <CardTitle>매출 추세</CardTitle>
        </CardHeader>
        <CardContent>
          <div class="h-64 bg-muted rounded-lg flex items-center justify-center">
            <div class="text-center">
              <Icon name="trending-up" class="h-12 w-12 text-muted-foreground mx-auto mb-2" />
              <p class="text-muted-foreground">차트 라이브러리 연동 필요</p>
              <p class="text-sm text-muted-foreground">Chart.js 또는 다른 차트 라이브러리를 추가하세요</p>
            </div>
          </div>
        </CardContent>
      </Card>
    </div>
  </NuxtLayout>
</template>

<script setup lang="ts">
import { cn } from '~/lib/utils'

// SEO
useHead({
  title: '대시보드 - Shashboard'
})

// Sample data
const stats = [
  {
    title: '총 매출',
    value: '₩45,231,890',
    change: 20.1,
    icon: 'dollar-sign'
  },
  {
    title: '방문자 수',
    value: '+2,350',
    change: 180.1,
    icon: 'users-2'
  },
  {
    title: '새 가입자',
    value: '+12,234',
    change: 19.0,
    icon: 'users'
  },
  {
    title: '알림',
    value: '573',
    change: -2.0,
    icon: 'bell'
  }
]

const recentActivity = [
  {
    id: 1,
    user: '김철수',
    action: '로그인',
    time: '2분 전',
    status: '성공'
  },
  {
    id: 2,
    user: '박영희',
    action: '프로필 업데이트',
    time: '10분 전',
    status: '성공'
  },
  {
    id: 3,
    user: '이민수',
    action: '결제 시도',
    time: '15분 전',
    status: '실패'
  },
  {
    id: 4,
    user: '정수진',
    action: '계정 생성',
    time: '1시간 전',
    status: '성공'
  },
  {
    id: 5,
    user: '최영수',
    action: '비밀번호 재설정',
    time: '2시간 전',
    status: '성공'
  }
]
</script>
