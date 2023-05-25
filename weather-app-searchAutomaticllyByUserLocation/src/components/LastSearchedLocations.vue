<template>
  <div class="last-searched-locations">
    <h3 v-if="locations.length > 0"></h3>
    <div class="buttons-container">
      <button v-for="(location, index) in lastSearchedLocations" :key="index" @click="handleSearch(location)">
        {{ location }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    locations: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      lastSearchedLocations: ['city-1', 'city-2', 'city-3'],
    };
  },
  methods: {
    handleSearch(location) {
      this.$emit('searchWeather', location);
    },
  },
  computed: {
    lastSearchedLocations() {
      const lastLocations = [...this.locations].reverse().slice(0, 3);
      return ['city-1', 'city-2', 'city-3'].map((city, index) => {
        if (index < lastLocations.length) {
          return lastLocations[index];
        }
        return city;
      });
    },
  },
};
</script>

<style scoped>
.last-searched-locations {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.last-searched-locations h3 {
  margin-bottom: 10px;
}

.buttons-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: 90%;
  max-width: 600px;
  /* Optionally, set a max-width for better responsiveness */
  margin-left: auto;
  /* Center the container horizontally */
  margin-right: auto;
  /* Center the container horizontally */
}

.buttons-container button {
  margin-bottom: 10px;
  flex: 1;
  /* Distribute the available width equally among buttons */
  padding: 5px 10px;
  font-size: 14px;
  background-color: #575555;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
