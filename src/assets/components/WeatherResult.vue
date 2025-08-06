<template>
  <div v-if="coordinates" class="weather_results">
    <h3 class="text-xl font-bold mb-2">{{ district }} Weather</h3>
    <div v-if="isLoading">Loading...</div>
    <div v-else-if="error">Error: {{ error }}</div>
    <div v-else-if="weatherData" class="weather_data">
      <p><strong>Condition:</strong> {{ weatherData.condition }}</p>
      <p><strong>Temperature:</strong> {{ weatherData.temperature }} °C</p>
      <p><strong>Humidity:</strong> {{ weatherData.humidity }}%</p>
      <p><strong>Wind Speed:</strong> {{ weatherData.wind }} m/s</p>
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
  0: "Clear sky",
  1: "Mainly clear",
  2: "Partly cloudy",
  3: "Overcast",
  45: "Fog",
  48: "Depositing rime fog",
  51: "Light drizzle",
  53: "Moderate drizzle",
  55: "Dense drizzle",
  56: "Light freezing drizzle",
  57: "Dense freezing drizzle",
  61: "Slight rain",
  63: "Moderate rain",
  65: "Heavy rain",
  66: "Light freezing rain",
  67: "Heavy freezing rain",
  71: "Slight snow fall",
  73: "Moderate snow fall",
  75: "Heavy snow fall",
  77: "Snow grains",
  80: "Slight rain showers",
  81: "Moderate rain showers",
  82: "Violent rain showers",
  85: "Slight snow showers",
  86: "Heavy snow showers",
  95: "Thunderstorm",
  96: "Thunderstorm with slight hail",
  99: "Thunderstorm with heavy hail"
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
        // Find the closest hour
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

    weatherData.value = {
      temperature: data.current_weather.temperature,
      humidity,
      wind: data.current_weather.windspeed,
      condition: weatherCodeMap[data.current_weather.weathercode] ?? data.current_weather.weathercode,
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
  margin-left: 43%;
}
</style>

