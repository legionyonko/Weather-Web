<template>
  <div>
    <label>Select State:</label>
    <select v-model="selectedState">
      <option disabled value="">-- Choose State --</option>
      <option v-for="(data, state) in locations" :key="state" :value="state">
        {{ state }}
      </option>
    </select>
    <div v-if="flag" style="margin-top:10px">
      <img :src="flag" alt="Flag" style="width:100px; height:auto" />
    </div>
  </div>
</template>

<script>
import { locations } from '../data/locations'

export default {
  props: ['modelValue'],
  emits: ['update:modelValue'],
  computed: {
    selectedState: {
      get() {
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    },
    flag() {
      return this.selectedState ? locations[this.selectedState]?.flag : ''
    }
  }
}
</script>

