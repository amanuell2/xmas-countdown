<script setup>
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'
import { computed } from 'vue'

const now = useNow()
const christmas = new Date('12/25/2022 00:00:00')

const days = computed(() => {
  const one_day = 1000 * 60 * 60 * 24
  return (christmas.getTime() - now.value.getTime()) / one_day
})
const daysRounded = computed(() => {
  return Math.floor(days.value)
})

const hours = computed(() => {
  return 24 * (days.value - daysRounded.value)
})
const hourRounded = computed(() => {
  return Math.floor(hours.value)
})

const minutes = computed(() => {
  return 60 * (hours.value - hourRounded.value)
})
const minutesRounded = computed(() => {
  return Math.floor(minutes.value)
})

const seconds = computed(() => {
  return 60 * (minutes.value - minutesRounded.value)
})
const secondsRounded = computed(() => {
  return Math.floor(seconds.value)
})
</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number="daysRounded" />
          <CountdownSegment label="hours" :number="hourRounded" />
          <CountdownSegment label="minutes" :number="minutesRounded" />
          <CountdownSegment label="seconds" :number="secondsRounded" />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
