<template>
  <div>
    <label>Select Option:</label>
    <select v-model="selectedOption">
      <option disabled value="">-- Choose Option --</option>
      <option value="temperature">Temperature</option>
      <option value="humidity">Humidity</option>
      <option value="wind">Wind Speed</option>
    </select>
  </div>
</template>

<script>
export default {
  props: ['modelValue'],
  emits: ['update:modelValue'],
  computed: {
    selectedOption: {
      get() {
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    }
  }
}
</script>
