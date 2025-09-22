<script setup>
defineProps({
  location: String,
  weatherData: Object,
  loading: Boolean,
  error: String
})

defineEmits(['search', 'update:location'])
</script>

<template>
  <div class="weather-app">
    <div class="search-box">
      <input 
        :value="location" 
        @input="$emit('update:location', $event.target.value)"
        @keyup.enter="$emit('search')" 
        placeholder="Cari lokasi..."
      >
      <button @click="$emit('search')">Cari</button>
    </div>
    
    <div v-if="loading" class="weather-info">
      Memuat data cuaca...
    </div>
    
    <div v-else-if="error" class="weather-info error">
      {{ error }}
    </div>
    
    <div v-else-if="weatherData" class="weather-info">
      <div class="location">{{ weatherData.name }}</div>
      <img 
        :src="`https://openweathermap.org/img/wn/${weatherData.weather[0].icon}@2x.png`" 
        :alt="weatherData.weather[0].description"
        class="weather-icon"
      >
      <div class="temperature">{{ Math.round(weatherData.main.temp) }}°C</div>
      <div class="description">{{ weatherData.weather[0].description }}</div>
      
      <div class="details">
        <div class="detail-item">
          <div class="detail-label">Kelembaban</div>
          <div class="detail-value">{{ weatherData.main.humidity }}%</div>
        </div>
        <div class="detail-item">
          <div class="detail-label">Angin</div>
          <div class="detail-value">{{ Math.round(weatherData.wind.speed * 3.6) }} km/h</div>
        </div>
        <div class="detail-item">
          <div class="detail-label">Terasa</div>
          <div class="detail-value">{{ Math.round(weatherData.main.feels_like) }}°C</div>
        </div>
      </div>
    </div>
    
    <div v-else class="weather-info">
      Masukkan lokasi untuk melihat cuaca
    </div>
  </div>
</template>

<style scoped>
.weather-app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-image: url('https://source.unsplash.com/1600x900/?weather,snow');
  background-size: cover;
  background-position: center;
  padding: 20px;
  color: white;
  text-shadow: 1px 1px 2px #000;
}

.search-box {
  background-color: rgba(255, 255, 255, 0.2);
  padding: 10px;
  border-radius: 10px;
  display: flex;
  backdrop-filter: blur(10px);
  margin-bottom: 30px;
}

.search-box input {
  padding: 10px;
  border: none;
  border-radius: 10px 0 0 10px;
  outline: none;
  font-size: 16px;
  background-color: rgba(255, 255, 255, 0.6);
  color: #000;
}

.search-box button {
  padding: 10px 15px;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 0 10px 10px 0;
  cursor: pointer;
  font-weight: bold;
}

.weather-info {
  text-align: center;
}

.location {
  font-size: 48px;
  font-weight: bold;
  margin-bottom: 10px;
}

.weather-icon {
  width: 80px;
  height: 80px;
}

.description {
  font-size: 24px;
  margin: 10px 0;
  text-transform: capitalize;
}

.temperature {
  font-size: 48px;
  font-weight: bold;
  margin: 10px 0;
}

.details {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-top: 30px;
  flex-wrap: wrap;
}

.detail-item {
  background-color: rgba(0, 0, 0, 0.7);
  padding: 15px 20px;
  border-radius: 15px;
  min-width: 100px;
  text-align: center;
}

.detail-label {
  font-size: 14px;
  color: #ccc;
  margin-bottom: 5px;
}

.detail-value {
  font-size: 24px;
  font-weight: bold;
}

.error {
  background-color: rgba(255, 0, 0, 0.5);
  padding: 10px;
  border-radius: 10px;
  font-weight: bold;
}

</style>