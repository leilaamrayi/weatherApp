<template>
  <div id="app">
    <div class="container">
      <Logo />
      <LastSearchedLocations :locations="lastSearchedLocations" @searchWeather="searchWeather" />
      <SearchInput :locations="lastSearchedLocations" @search="searchWeather" />
      <WeatherResult v-if="weatherData" :currentWeather="weatherData" :hourlyForecast="hourlyForecast" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import axios from 'axios';
import Logo from './components/Logo.vue';
import LastSearchedLocations from './components/LastSearchedLocations.vue';
import SearchInput from './components/SearchInput.vue';
import WeatherResult from './components/WeatherResult.vue';

interface WeatherData {
  main: {
    temp: number;
    humidity: number;
    pressure: number;
  };
  weather: {
    icon: string;
    description: string;
  }[];
  wind: {
    speed: number;
  };
}

interface Forecast {
  dt: number;
  weather: {
    icon: string;
    description: string;
  }[];
  main: {
    temp: number;
  };
}

export default defineComponent({
  name: 'App',
  components: {
    Logo,
    LastSearchedLocations: LastSearchedLocations as any, // Provide type information
    SearchInput: SearchInput as any, // Provide type information
    WeatherResult,
  },
  setup() {
    const lastSearchedLocations = ref<string[]>([]);
    const weatherData = ref<WeatherData | null>(null);
    const hourlyForecast = ref<Forecast[]>([]);
    const inputValue = ref('');

    const searchWeather = (location: string) => {
      getWeatherData(location);
      getHourlyForecast(location);
      updateLastSearchedLocations(location);
    };

    const getWeatherData = (location: string) => {
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${location}&appid=da2c5748f467c455a89d0b1a2e32a0b2&units=metric`;
      axios
        .get(url)
        .then((response) => {
          weatherData.value = response.data;
        })
        .catch((error) => {
          console.error('Error fetching weather data:', error);
        });
    };

    const getHourlyForecast = (location: string) => {
      const url = `https://api.openweathermap.org/data/2.5/forecast?q=${location}&appid=da2c5748f467c455a89d0b1a2e32a0b2&units=metric`;
      axios
        .get(url)
        .then((response) => {
          hourlyForecast.value = response.data.list;
        })
        .catch((error) => {
          console.error('Error fetching hourly forecast:', error);
        });
    };

    const updateLastSearchedLocations = (location: string) => {
      const index = lastSearchedLocations.value.indexOf(location);
      if (index !== -1) {
        lastSearchedLocations.value.splice(index, 1);
      }
      lastSearchedLocations.value.unshift(location);
      if (lastSearchedLocations.value.length > 3) {
        lastSearchedLocations.value.pop();
      }
    };

    const updateInput = (location: string) => {
      inputValue.value = location;
    };

    return {
      lastSearchedLocations,
      weatherData,
      hourlyForecast,
      inputValue,
      searchWeather,
      updateInput,
    };
  },
});
</script>

<style>
#app {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #f8f8f8;
}

.container {
  max-width: 600px;
  padding: 0px;
  text-align: center;
  background-color: #e4dada;

}
</style>
