<template>
  <div class="weather-details active">
    <div class="humidity">
      <i class="bx bx-water"></i>
      <div class="text">
        <div class="info-humidity"><span>{{ weatherData.main.humidity }}%</span></div>
        <p>Humidity</p>
      </div>
    </div>
    <div class="wind">
      <i class="bx bx-wind"></i>
      <div class="text">
        <div class="info-wind"><span>{{ Math.round(weatherData.wind.speed) }}Km/h</span></div>
        <p>Wind Speed</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["weatherData"],
};
</script>
