<template>
  <div class="search-box">
    <i class="bx bx-map"></i>
    <input v-model="searchQuery" type="text" placeholder="Enter Your Location" @keyup.enter="searchWeather" />
    <button class="bx bx-search-alt" @click="searchWeather"></button>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  emits: ["search"],
  setup(_, { emit }) {
    const searchQuery = ref("");

    const searchWeather = () => {
      if (searchQuery.value.trim() !== "") {
        emit("search", searchQuery.value);
      }
    };

    return { searchQuery, searchWeather };
  },
};
</script>
