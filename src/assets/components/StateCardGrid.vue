<template>
  <div class="p-4">
    <div class="state-container">
      <div v-for="(stateData, stateName) in filteredStates" :key="stateName" class="state-box"
        @click="$emit('select-state', stateName)">
        <img :src="stateData.flag" alt="flag" class="state_flag" />
        <div class="state_info">
          <h2 class="statename">{{ stateName }}</h2>
          <p class="num_district">{{ Object.keys(stateData.districts).length }} districts</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { locations } from '@/data/locations.js'

export default {
  props: {
    search: {
      type: String,
      default: ''
    }
  },
  computed: {
    filteredStates() {
      const term = this.search.toLowerCase()
      return Object.fromEntries(
        Object.entries(locations).filter(([name]) => name.toLowerCase().includes(term))
      )
    }
  }
}
</script>

<style scpoed>
.state-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.state-box {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 16px;
  margin: 8px;
  cursor: pointer;
  width: 200px;
  height: 200px;
  text-align: center;
  
}
.state_flag {
  width: 150px;
  height: auto;
} 
.state_info {
  margin-top: 8px;
}
.statename {
  font-size: 1.2em;
  font-weight: bold;
}
.num_district {
  color: #666;
}
</style>