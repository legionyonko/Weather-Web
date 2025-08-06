<template>
  <div v-if="state" class="district-selector">
    <label>Select District:</label>
    <select v-model="selectedDistrict">
      <option disabled value="" class="choose_district">-- Choose District --</option>
      <option v-for="(coords, district) in districts" :key="district" :value="district" class="district_option">
        {{ district }}
      </option>
    </select>
  </div>
</template>

<script>
import { locations } from '@/data/locations.js'

export default {
  props: ['state', 'modelValue'],
  emits: ['update:modelValue'],
  computed: {
    selectedDistrict: {
      get() {
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    },
    districts() {
      return this.state ? locations[this.state]?.districts || {} : {}
    }
  }
}
</script>

<style scoped>
.district-selector {
    margin-left: 650px;
    margin-top: 20px;
    width: 200px;
    height: 40px;

}
.choose_district{
    width:50px;
    height:20px;
    font-size: 16px;
}
.district_option {
    margin-left:45%;
    padding: 5px;
    font-size: 16px;
}
.district-selector select {
    width: 220px;   /* increase as needed */
    height: 30px;   /* increase as needed */
    font-size: 16px; /* make text bigger */
    padding: 6px 10px;
}
</style>
