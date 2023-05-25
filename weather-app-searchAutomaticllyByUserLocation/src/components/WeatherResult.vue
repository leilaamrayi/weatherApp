<template>
  <div class="weather-result">
    <div class="weather-info">
      <div class="weather-container">
        <div class="weather-icon-temp">
          <div class="weather-icon">
            <img :src="getWeatherIconUrl(currentWeather.weather[0].icon)" :alt="currentWeather.weather[0].description" />
          </div>
          <div class="temperature">
            <span class="temperature-value">{{ currentWeather.main.temp }}°C</span>
          </div>
        </div>

        <div class="weather-description">
          <p>Humidity: {{ currentWeather.main.humidity }}%</p>
          <p>Wind Speed: {{ currentWeather.wind.speed }} m/s</p>
          <p>Pressure: {{ currentWeather.main.pressure }} hPa</p>
        </div>
      </div>
    </div>
    <h3>Hourly Forecast</h3>
    <div class="hourly-forecast">
      <div v-for="forecast in hourlyForecast" :key="forecast.dt">
        <img :src="getWeatherIconUrl(forecast.weather[0].icon)" :alt="forecast.weather[0].description" />
        <p>Temperature: {{ forecast.main.temp }}°C</p>
        <p>Time: {{ formatTime(forecast.dt) }}</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

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
  name: 'WeatherResult',
  props: {
    currentWeather: {
      type: Object,
      required: true,
    },
    hourlyForecast: {
      type: Array as () => Forecast[], // Explicitly define the type as an array of Forecast
      required: true,
    },
  },

  methods: {
    getWeatherIconUrl(icon: string): string {
      return `https://openweathermap.org/img/wn/${icon}.png`;
    },
    formatTime(timestamp: number): string {
      const date = new Date(timestamp * 1000);
      return date.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
    },
  },
});
</script>


<style scoped>
.weather-result {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  margin-top: .5rem;
}

.weather-container {
  border: 1px solid #120707;
  border-radius: 4px;
  width: 90%;
}

.weather-icon-temp {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  align-items: center;
  text-align: center;

}

.weather-info {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1rem;
  padding: 1rem;
  width: 100%;
}


.weather-icon img {
  width: 70px;
  height: 70px;
}

.temperature {
  font-size: 22px;
  color: #333;
  margin-left: 10rem;
}

.weather-description {
  margin-bottom: 2rem;
  font-size: 18px;
  color: #333;
}

.hourly-forecast {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  border: 1px solid #120707;
  border-radius: 4px;
  width: 90%;
}

.hourly-forecast img {
  width: 50px;
  height: 50px;
}

.hourly-forecast p {
  margin: 0;
}
</style>
