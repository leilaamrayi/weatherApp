<template>
  <div class="search-input">
    <input ref="searchInput" type="text" v-model="location" @blur="search" @input="resetTimer" placeholder="Enter a location" />
    <p class="error-message" v-if="showErrorMessage">Invalid location. Please try again.</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import axios from 'axios';

export default defineComponent({
  data() {
    return {
      location: '',
      showErrorMessage: false,
      timer: undefined as ReturnType<typeof setTimeout> | undefined,
    };
  },
  mounted() {
    const urlParams = new URLSearchParams(window.location.search);
    const locationParam = urlParams.get('location');
    if (locationParam) {
      this.location = locationParam;
    }
  },
  methods: {
    search() {
      if (this.location.trim() !== '') {
        this.getWeatherData();
      }
    },
    resetTimer() {
      clearTimeout(this.timer);
      this.timer = setTimeout(() => {
        this.search();
      }, 2000);
    },
    getWeatherData() {
      const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=da2c5748f467c455a89d0b1a2e32a0b2&units=metric`;

      axios
        .get(apiUrl)
        .then((response) => {
          const retrievedLocation = response.data.name;
          if (this.location.toLowerCase() === retrievedLocation.toLowerCase()) {
            this.showErrorMessage = false;
            this.$emit('search', this.location);
            this.location = ''; // Clear the input field after search
          } else {
            this.showErrorMessage = true;
          }
        })
        .catch((error) => {
          console.error('Error fetching weather data:', error);
          this.showErrorMessage = true;
        });
    },
  },
});
</script>

<style scoped>
.search-input input {
  padding: 5px 10px;
  font-size: 14px;
  border: 1px solid #020202;
  border-radius: 4px;
  width: 90%;
  box-sizing: border-box;
  background-color: #e4dada;
  color: black;
}

.error-message {
  color: red;
  margin-top: 5px;
  font-size: 14px;
}
</style>
