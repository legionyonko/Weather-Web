<template>
  <div>
    <div class="top-banner">
      <h1 class="header">Weather In Malaysia</h1>
      
      <input v-model="search" type="text" placeholder="Search state..." class="search_box" v-if="!selectedState" />
    </div>
    <StateCardGrid @select-state="selectedState = $event" v-if="!selectedState" :search="search" />
    <div v-else>
      <p class="selectedState">Selected State: {{ selectedState }}</p>
      <p class="selectedDistrict">Selected District: {{ selectedDistrict }}</p>
      <button @click="selectedState = null" class="back-to-states">&larr; Back to States</button>
      <DistrictSelector :state="selectedState" v-model="selectedDistrict" />
      <WeatherResult v-if="selectedDistrict" :state="selectedState" :district="selectedDistrict"
        :coordinates="selectedCoordinates" />
    </div>
  </div>
</template>

<script>
import StateCardGrid from './assets/components/StateCardGrid.vue'
import DistrictSelector from './assets/components/DistrictSelector.vue'
import WeatherResult from './assets/components/WeatherResult.vue'
import { locations } from './data/locations.js'

export default {
  components: {
    StateCardGrid,
    DistrictSelector,
    WeatherResult
  },
  data() {
    return {
      search: '',
      selectedState: null,
      selectedDistrict: null
    }
  },
  computed: {
    selectedCoordinates() {
      if (
        this.selectedState &&
        this.selectedDistrict &&
        locations[this.selectedState] &&
        locations[this.selectedState].districts[this.selectedDistrict]
      ) {
        return locations[this.selectedState].districts[this.selectedDistrict];
      }
      return null;
    }
  }
}
</script>

<style scoped>
.top-banner {
  height:400px ;
  text-align: center;
  margin-bottom: 20px;
  background-image: url('https://www.pelago.com/img/countries/malaysia/0727-1550_malaysia.jpg');
  background-size: cover;
  background-position: top right bottom left;
  background-repeat: no-repeat; 
  padding: 40px 0 30px 0;
  color: white; 
} 
.header {
  font-size: 4em;
  margin-bottom: 10px;
  
} 
.search_box {
  width: 300px;
  padding: 10px;
  font-size: 1em;
  border-radius: 5px;
  border: 1px solid #ccc;
}
.state-box {
  cursor: pointer; 
  transition: transform 0.2s;
} 
.state-box:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 8px rgb(255, 255, 255);
}
.selectedState {
  font-size: 1.5em;
  margin: 20px 45%;
  
}
.selectedDistrict {
  font-size: 1.5em;
  margin: 20px 45%;
}
.back-to-states {
  position: absolute;
  top: 20px;
  left: 20px;
  margin-top: 0;
  z-index: 10;
}

</style>