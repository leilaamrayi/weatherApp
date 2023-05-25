<template>
  <h3 class="logo">{{ title }}</h3>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Logo',
  data() {
    return {
      title: 'Awesome Weather App',
    };
  },
});
</script>

<style scoped>
.logo {
  font-size: 30px;
  color: #ffffff;
  text-align: center;
  margin: 0;
  padding: 10px 10px;
  width: 100%;
  box-sizing: border-box;
  background-color: #575555;
  border: none;
  border-radius: 4px;
}
</style>








