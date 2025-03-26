<template>
  <div class="container">
    <SearchBox @search="fetchWeather" />
    <p class="city-hide">{{ city }}</p>
    <WeatherBox v-if="weatherData" :weatherData="weatherData" />
    <WeatherDetails v-if="weatherData" :weatherData="weatherData" />
    <NotFound v-if="error" />
  </div>
</template>

<script>
import { ref } from "vue";
import SearchBox from "./components/SearchBox.vue";
import WeatherBox from "./components/WeatherBox.vue";
import WeatherDetails from "./components/WeatherDetails.vue";
import NotFound from "./components/NotFound.vue";

export default {
  components: { SearchBox, WeatherBox, WeatherDetails, NotFound },
  setup() {
    const city = ref("");
    const weatherData = ref(null);
    const error = ref(false);
    const APIKey = "bdb4d953d6e29d42f78211d066a7b96f";

    const fetchWeather = async (searchCity) => {
      if (!searchCity) return;
      city.value = searchCity;
      error.value = false;

      try {
        const res = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${searchCity}&units=metric&appid=${APIKey}`
        );
        const data = await res.json();

        if (data.cod === "404") {
          error.value = true;
          weatherData.value = null;
        } else {
          weatherData.value = data;
        }
      } catch (err) {
        console.error("Error fetching data:", err);
        error.value = true;
      }
    };

    return { city, weatherData, error, fetchWeather };
  },
};
</script>

<style scoped>
@import "./style.css";
</style>
