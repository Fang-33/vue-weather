<script setup>
import { onMounted, ref } from 'vue';
import HeaderInfo from './components/HeaderInfo.vue';
import CurrentWeather from './components/CurrentWeather.vue';
import { useWeatherStore } from "./stores/currentWeather.js"



// 取用 store
const weatherStore = useWeatherStore()

// 打 js 原生方法取得目前座標
const getLocation = () => new Promise((resolve, reject) => {
  navigator.geolocation.getCurrentPosition(
    (position) => {
      weatherStore.setLocation(position.coords)
      resolve(position)
    },
    (err) => {
      weatherStore.setErrorMsg(`無法取得位置: ${err.message}`)
      reject(err)
    }
  )
})


onMounted(async () => {
  await getLocation()
  if (weatherStore.location) {
    await weatherStore.fetchWeatherData()
  }
  if (weatherStore.location) {
    await weatherStore.fetchLocation()
  }
})

</script>

<template>
  <main class="bg-cyan-600  h-screen  flex flex-col justify-center items-center">
    <HeaderInfo />
    <CurrentWeather />
  </main>


</template>

<style scoped></style>
