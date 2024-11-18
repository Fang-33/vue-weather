<script setup>
import { ref } from "vue"
import { Iconoir, Cloud } from '@iconoir/vue';
import { storeToRefs } from 'pinia';
import { useWeatherStore } from '@/stores/currentWeather';

const weatherStore = useWeatherStore()
const { currentWeather } = storeToRefs(weatherStore)

</script>


<!-- 如果 api 成功打這個 -->
<!-- `https://openweathermap.org/img/wn/${currentWeather.weather[0].icon}@2x.png` -->
<template>
  <!-- {{ currentWeather.weather[0].icon }} -->
  <div class="flex flex-col items-center gap-y-4 mt-10">
    <!-- <Cloud color="#ded8d8" width="60" height="60" /> -->
    <img v-if="currentWeather?.weather?.[0]?.icon"
      :src="`https://openweathermap.org/img/wn/${currentWeather.weather[0].icon}@2x.png`"
      class="w-40 h-40">
    <img v-else :src="`https://openweathermap.org/img/wn/03d@2x.png`" class="w-40 h-40">
    <div v-if="currentWeather" class="flex flex-col items-center">
      <p class="text-6xl font-bold text-white">{{ (currentWeather.temp - 273.15).toFixed(2) }}°C</p>
      <p class="text-xl  text-gray-300">{{ currentWeather.weather[0].description }}</p>
    </div>
    <div v-else>
      <p class="text-6xl font-bold text-white">33.33°</p>
      <p class="text-xl  text-gray-300">Rain</p>
    </div>

  </div>


</template>