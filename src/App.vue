<template>
  <div class="container" :class="{ active: isActive }">
    <SearchBox @search="fetchWeatherData" />
    
    <WeatherBox 
      v-if="weatherData" 
      :weatherData="weatherData" 
      :icon="weatherIcon" 
    />

    <WeatherDetails 
      v-if="weatherData" 
      :humidity="weatherData.main.humidity" 
      :windSpeed="weatherData.wind.speed" 
    />

    <NotFound v-if="notFound" />
  </div>
</template>

<script>
import { ref } from 'vue';
import SearchBox from './components/SearchBox.vue';
import WeatherBox from './components/WeatherBox.vue';
import WeatherDetails from './components/WeatherDetails.vue';
import NotFound from './components/NotFound.vue';

export default {
  components: {
    SearchBox,
    WeatherBox,
    WeatherDetails,
    NotFound,
  },
  setup() {
    const APIKey = 'bdb4d953d6e29d42f78211d066a7b96f';
    const weatherData = ref(null);
    const weatherIcon = ref('');
    const notFound = ref(false);
    const isActive = ref(false);

    const fetchWeatherData = async (city) => {
      if (!city) return;

      try {
        const response = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${APIKey}`
        );
        const data = await response.json();

        if (data.cod === '404') {
          weatherData.value = null;
          notFound.value = true;
          isActive.value = false;
          return;
        }

        weatherData.value = data;
        notFound.value = false;
        isActive.value = true;

        switch (data.weather[0].main) {
          case 'Clear': weatherIcon.value = '/images/clear.png'; break;
          case 'Clouds': weatherIcon.value = '/images/cloud.png'; break;
          case 'Mist':
          case 'Haze': weatherIcon.value = '/images/mist.png'; break;
          case 'Rain': weatherIcon.value = '/images/rain.png'; break;
          case 'Snow': weatherIcon.value = '/images/snow.png'; break;
          default: weatherIcon.value = '/images/cloud.png';
        }

        setTimeout(() => {
          isActive.value = false;
        }, 2500);
      } catch (error) {
        console.error('Error fetching weather data:', error);
      }
    };

    return { weatherData, weatherIcon, notFound, isActive, fetchWeatherData };
  },
};
</script>
