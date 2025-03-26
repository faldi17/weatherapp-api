<template>
  <div class="weather-details">
    <div class="humidity">
      <i class="bx bx-water"></i>
      <div class="text">
        <span>{{ humidity }}%</span>
        <p>Humidity</p>
      </div>
    </div>
    <div class="wind">
      <i class="bx bx-wind"></i>
      <div class="text">
        <span>{{ windSpeed }}Km/h</span>
        <p>Wind Speed</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['humidity', 'windSpeed'],
};
</script>
