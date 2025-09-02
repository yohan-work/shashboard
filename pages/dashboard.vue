<template>
  <NuxtLayout name="dashboard">
    <div class="space-y-8 p-8 bg-background min-h-screen">
      <!-- Stats Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        <div
          v-for="stat in stats"
          :key="stat.title"
          class="stat-card group cursor-pointer"
        >
          <div class="flex items-start justify-between mb-4">
            <div class="flex items-center space-x-2">
              <Icon :name="stat.icon" class="h-5 w-5 text-muted-foreground" />
              <span class="stat-label">{{ stat.title }}</span>
            </div>
            <Icon name="trending-up" class="h-4 w-4 text-muted-foreground" />
          </div>

          <div class="space-y-2">
            <div class="stat-value">{{ stat.value }}</div>
            <div class="flex items-center space-x-2">
              <span
                :class="
                  cn('stat-change', stat.change > 0 ? 'positive' : 'negative')
                "
              >
                {{ stat.change > 0 ? "+" : "" }}{{ stat.change }}%
              </span>
              <span class="text-xs text-muted-foreground">{{
                stat.period
              }}</span>
            </div>
            <p class="text-xs text-muted-foreground leading-relaxed">
              {{ stat.description }}
            </p>
          </div>
        </div>
      </div>

      <!-- Chart Section -->
      <Card class="bg-card border border-border">
        <div class="p-6">
          <div class="flex items-center justify-between mb-6">
            <div>
              <h3 class="text-xl font-semibold text-foreground mb-2">
                Total Visitors
              </h3>
              <p class="text-sm text-muted-foreground">
                Total for the last 3 months
              </p>
            </div>
            <div class="flex space-x-2">
              <Button
                v-for="period in chartPeriods"
                :key="period.value"
                :variant="
                  selectedPeriod === period.value ? 'default' : 'outline'
                "
                size="sm"
                class="text-xs"
                @click="selectedPeriod = period.value"
              >
                {{ period.label }}
              </Button>
            </div>
          </div>

          <!-- Chart Placeholder with realistic design -->
          <div
            class="h-80 bg-background border border-border rounded-lg p-4 relative overflow-hidden"
          >
            <!-- Chart Background Grid -->
            <div class="absolute inset-4 opacity-20">
              <div class="h-full w-full relative">
                <!-- Horizontal grid lines -->
                <div
                  v-for="i in 6"
                  :key="i"
                  class="absolute w-full border-t border-muted"
                  :style="{ top: `${(i - 1) * 20}%` }"
                ></div>
                <!-- Vertical grid lines -->
                <div
                  v-for="i in 12"
                  :key="'v' + i"
                  class="absolute h-full border-l border-muted"
                  :style="{ left: `${(i - 1) * 8.33}%` }"
                ></div>
              </div>
            </div>

            <!-- Mock Chart Data Visualization -->
            <div class="absolute inset-4 flex items-end space-x-1">
              <!-- Chart bars/areas would go here -->
              <div
                v-for="(point, index) in chartData"
                :key="index"
                class="flex-1 relative"
              >
                <!-- Primary area -->
                <div
                  class="bg-gradient-to-t from-blue-500/20 to-blue-500/5 rounded-t-sm border-t-2 border-blue-400"
                  :style="{ height: `${point.primary}%` }"
                ></div>
                <!-- Secondary area -->
                <div
                  class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-green-500/20 to-green-500/5 rounded-t-sm border-t-2 border-green-400"
                  :style="{ height: `${point.secondary}%` }"
                ></div>
              </div>
            </div>

            <!-- Chart X-axis labels -->
            <div
              class="absolute bottom-1 left-4 right-4 flex justify-between text-xs text-muted-foreground"
            >
              <span v-for="label in xAxisLabels" :key="label">{{ label }}</span>
            </div>

            <!-- Chart legend -->
            <div class="absolute top-4 right-4 flex space-x-4">
              <div class="flex items-center space-x-2">
                <div class="w-3 h-3 bg-blue-400 rounded-full"></div>
                <span class="text-xs text-muted-foreground">Desktop</span>
              </div>
              <div class="flex items-center space-x-2">
                <div class="w-3 h-3 bg-green-400 rounded-full"></div>
                <span class="text-xs text-muted-foreground">Mobile</span>
              </div>
            </div>
          </div>
        </div>
      </Card>
    </div>
  </NuxtLayout>
</template>

<script setup lang="ts">
import { cn } from "~/lib/utils";

// SEO
useHead({
  title: "대시보드 - Shashboard",
});

// Chart period selection
const selectedPeriod = ref("3months");
const chartPeriods = [
  { value: "3months", label: "Last 3 months" },
  { value: "30days", label: "Last 30 days" },
  { value: "7days", label: "Last 7 days" },
];

// Stats data matching the image
const stats = [
  {
    title: "Total Revenue",
    value: "$1,250.00",
    change: 12.5,
    period: "this month",
    description: "Trending up this month",
    icon: "dollar-sign",
  },
  {
    title: "New Customers",
    value: "1,234",
    change: -20,
    period: "this period",
    description: "Down 20% this period",
    icon: "users",
  },
  {
    title: "Active Accounts",
    value: "45,678",
    change: 12.5,
    period: "Strong user retention",
    description: "Engagement exceed targets",
    icon: "users-2",
  },
  {
    title: "Growth Rate",
    value: "4.5%",
    change: 4.5,
    period: "Steady performance",
    description: "Meets growth projections",
    icon: "trending-up",
  },
];

// Mock chart data for visualization
const chartData = ref([
  { primary: 40, secondary: 25 },
  { primary: 65, secondary: 35 },
  { primary: 35, secondary: 20 },
  { primary: 80, secondary: 45 },
  { primary: 55, secondary: 30 },
  { primary: 75, secondary: 40 },
  { primary: 90, secondary: 60 },
  { primary: 70, secondary: 45 },
  { primary: 85, secondary: 55 },
  { primary: 95, secondary: 70 },
  { primary: 60, secondary: 35 },
  { primary: 50, secondary: 30 },
  { primary: 75, secondary: 50 },
  { primary: 80, secondary: 55 },
  { primary: 45, secondary: 25 },
  { primary: 70, secondary: 40 },
  { primary: 85, secondary: 60 },
  { primary: 90, secondary: 65 },
  { primary: 55, secondary: 35 },
  { primary: 75, secondary: 50 },
  { primary: 85, secondary: 55 },
  { primary: 70, secondary: 45 },
  { primary: 80, secondary: 50 },
  { primary: 65, secondary: 40 },
]);

// X-axis labels for the chart
const xAxisLabels = [
  "Jun 1",
  "Jun 3",
  "Jun 5",
  "Jun 7",
  "Jun 9",
  "Jun 12",
  "Jun 15",
  "Jun 18",
  "Jun 21",
  "Jun 24",
  "Jun 27",
  "Jun 30",
];
</script>
