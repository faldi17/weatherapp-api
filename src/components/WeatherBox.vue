<template>
  <div class="weather-box active">
    <div class="box">
      <div class="info-weather">
        <div class="weather">
          <img :src="weatherIcon" />
          <p class="temperature">{{ Math.round(weatherData.main.temp) }}<span>°C</span></p>
          <p class="description">{{ weatherData.weather[0].description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from "vue";

export default {
  props: ["weatherData"],
  setup(props) {
    const weatherIcon = computed(() => {
      const condition = props.weatherData.weather[0].main;
      switch (condition) {
        case "Clear":
          return "/images/clear.png";
        case "Clouds":
          return "/images/cloud.png";
        case "Mist":
        case "Haze":
          return "/images/mist.png";
        case "Rain":
          return "/images/rain.png";
        case "Snow":
          return "/images/snow.png";
        default:
          return "/images/cloud.png";
      }
    });

    return { weatherIcon };
  },
};
</script>
