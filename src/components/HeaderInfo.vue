<script setup>
import { ref } from "vue"
import { storeToRefs } from 'pinia';
import { useWeatherStore } from '@/stores/currentWeather';
import dayjs from 'dayjs'


const weatherStore = useWeatherStore()
const { city } = storeToRefs(weatherStore)

const now = dayjs().format("dddd, D MMMM, YYYY")
const currentDate = ref(now)

</script>


<template>
  <div class="flex flex-col gap-y-2  items-center">
    <h1 class="text-2xl font-semibold text-white">{{ city }}</h1>
    <p class="text-lg text-gray-200">{{ currentDate }}</p>
  </div>
</template>