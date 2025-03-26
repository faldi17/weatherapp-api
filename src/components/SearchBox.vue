<template>
  <div class="search-box">
    <i class="bx bx-map"></i>
    <input 
      type="text" 
      placeholder="Enter Your Location" 
      v-model="searchCity" 
      @keydown.enter="searchWeather"
    />
    <button class="bx bx-search-alt" @click="searchWeather"></button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  emits: ['search'],
  setup(_, { emit }) {
    const searchCity = ref('');

    const searchWeather = () => {
      if (searchCity.value.trim()) {
        emit('search', searchCity.value.trim());
      }
    };

    return { searchCity, searchWeather };
  },
};
</script>
