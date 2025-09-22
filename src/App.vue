<script setup>
import WeatherView from './views/WeatherView.vue'
</script>

<template>
  <div id="app">
    <video autoplay muted loop id="bg-video">
      <source src="https://cdn.pixabay.com/video/2017/05/14/9153-217588676_large.mp4" type="video/mp4">
    </video>
    <WeatherView />
  </div>
</template>

<style>
/* Gunakan font modern */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Inter', sans-serif;
}

html, body {
  height: 100%;
  width: 100%;
}

/* Video background styling */
#bg-video {
  position: fixed;
  right: 0;
  bottom: 0;
  min-width: 100%;
  min-height: 100%;
  z-index: -1;
  object-fit: cover;
}

/* Container utama responsif & modern */
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
  position: relative;
}
</style>