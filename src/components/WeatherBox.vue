<template>
  <div class="weather-box">
    <img :src="icon" />
    <p class="temperature">{{ Math.round(weatherData.main.temp) }}<span>°C</span></p>
    <p class="description">{{ weatherData.weather[0].description }}</p>
  </div>
</template>

<script>
export default {
  props: ['weatherData', 'icon'],
};
</script>
