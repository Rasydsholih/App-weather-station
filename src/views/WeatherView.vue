<script setup>
import { ref } from 'vue'
import WeatherDisplay from '../components/WeatherDisplay.vue'

const location = ref('bogor')
const weatherData = ref(null)
const loading = ref(false)
const error = ref(null)

const fetchWeather = async () => {
  if (!location.value) return
  
  loading.value = true
  error.value = null
  
  try {
    const response = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${location.value}&appid=b39e8f1e7ce1657ee6700d03eccdc213&units=metric`
    )
    
    if (!response.ok) {
      throw new Error('Lokasi tidak ditemukan')
    }
    
    const data = await response.json()
    weatherData.value = data
  } catch (err) {
    error.value = err.message
    weatherData.value = null
  } finally {
    loading.value = false
  }
}

// Fetch default location on component mount
fetchWeather()
</script>

<template>
  <div class="weather-view">
    <WeatherDisplay 
      :location="location"
      :weather-data="weatherData"
      :loading="loading"
      :error="error"
      @search="fetchWeather"
      @update:location="(val) => location = val"
    />
  </div>
</template>

<style scoped>
.weather-view {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
}
</style>