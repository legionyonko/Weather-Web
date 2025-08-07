<template>
  <div v-if="coordinates" class="weather_results">
    <h3 class="text-xl font-bold mb-2">{{ district }} Weather</h3>
    <div v-if="isLoading">Loading...</div>
    <div v-else-if="error">Error: {{ error }}</div>
    <div v-else-if="weatherData" class="weather_data">
      <img :src="`https://www.weatherbit.io/static/img/icons/${weatherData.icon}`" alt="weather icon"
        class="weather-icon mb-2" />
      <p><strong>Condition:</strong> {{ weatherData.condition }}</p>
      <p><strong>🌡️Temperature:</strong> {{ weatherData.temperature }} °C</p>
      <p><strong>💧Humidity:</strong> {{ weatherData.humidity }}%</p>
      <p><strong>🍃Wind Speed:</strong> {{ weatherData.wind }} m/s</p>
    </div>
  </div>
</template>

<script>
import { onMounted, ref, watch } from 'vue';

export default {
  props: ['district', 'coordinates', 'option'],
  setup(props) {
    const weatherData = ref(null);
    const isLoading = ref(false);
    const error = ref(null);

    const weatherCodeMap = {
      0: { desc: "Clear sky", icon: "c01d.png" },
      1: { desc: "Mainly clear", icon: "c02d.png" },
      2: { desc: "Partly cloudy", icon: "c02d.png" },
      3: { desc: "Overcast", icon: "c04d.png" },
      45: { desc: "Fog", icon: "a05d.png" },
      48: { desc: "Depositing rime fog", icon: "a05d.png" },
      51: { desc: "Light drizzle", icon: "d01d.png" },
      53: { desc: "Moderate drizzle", icon: "d02d.png" },
      55: { desc: "Dense drizzle", icon: "d03d.png" },
      56: { desc: "Light freezing drizzle", icon: "f01d.png" },
      57: { desc: "Dense freezing drizzle", icon: "f01d.png" },
      61: { desc: "Slight rain", icon: "r01d.png" },
      63: { desc: "Moderate rain", icon: "r02d.png" },
      65: { desc: "Heavy rain", icon: "r03d.png" },
      66: { desc: "Light freezing rain", icon: "f01d.png" },
      67: { desc: "Heavy freezing rain", icon: "f01d.png" },
      71: { desc: "Slight snow fall", icon: "s01d.png" },
      73: { desc: "Moderate snow fall", icon: "s02d.png" },
      75: { desc: "Heavy snow fall", icon: "s03d.png" },
      77: { desc: "Snow grains", icon: "s05d.png" },
      80: { desc: "Slight rain showers", icon: "r01d.png" },
      81: { desc: "Moderate rain showers", icon: "r02d.png" },
      82: { desc: "Violent rain showers", icon: "r03d.png" },
      85: { desc: "Slight snow showers", icon: "s01d.png" },
      86: { desc: "Heavy snow showers", icon: "s03d.png" },
      95: { desc: "Thunderstorm", icon: "t04d.png" },
      96: { desc: "Thunderstorm with slight hail", icon: "t04d.png" },
      99: { desc: "Thunderstorm with heavy hail", icon: "t04d.png" }
    };

    const fetchWeather = async () => {
      if (!props.coordinates) return;
      isLoading.value = true;
      error.value = null;

      try {
        const { lat, lon } = props.coordinates;
        const response = await fetch(
          `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current_weather=true&hourly=relative_humidity_2m`
        );
        const data = await response.json();
        if (!data.current_weather) throw new Error('No weather data found');

        let humidity = 'N/A';
        if (data.hourly && data.hourly.time && data.hourly.relative_humidity_2m) {
          const currentTime = new Date(data.current_weather.time).getTime();
          let minDiff = Infinity;
          let closestIdx = -1;

          data.hourly.time.forEach((t, idx) => {
            const diff = Math.abs(new Date(t).getTime() - currentTime);
            if (diff < minDiff) {
              minDiff = diff;
              closestIdx = idx;
            }
          });

          if (closestIdx !== -1) {
            humidity = data.hourly.relative_humidity_2m[closestIdx];
          }
        }

        const code = data.current_weather.weathercode;
        const conditionData = weatherCodeMap[code] || {
          desc: `Code ${code}`,
          icon: "unknown.png"
        };

        weatherData.value = {
          temperature: data.current_weather.temperature,
          humidity,
          wind: data.current_weather.windspeed,
          condition: conditionData.desc,
          icon: conditionData.icon // just the filename, e.g. "c01d.png"
        };
      } catch (err) {
        error.value = err.message;
      } finally {
        isLoading.value = false;
      }
    };

    onMounted(fetchWeather);
    watch(() => props.coordinates, fetchWeather);

    return {
      weatherData,
      isLoading,
      error
    };
  }
};
</script>

<style scoped>
.weather_results {
  margin-top: 50px;
  font-size: 20px;
  margin-left: 1%;
  margin-bottom: 50px;
  text-align: center;
}
</style>
