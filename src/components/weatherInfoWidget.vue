<template>
  <div class="container">
    <div class="alert alert-info text-center" role="alert">
      <p>City: {{ forecast.cityName }}</p>
      <p>Temperature: {{ forecast.temperature | toCelcius }} &deg;C</p>
      <p>Wind Speed: {{ forecast.windSpeed | toKmHr}} km/hr</p>
      <p>Weather Info: {{ forecast.main }} - "{{ forecast.description }}"</p>
    </div>
    <div class="alert alert-danger" role="alert" v-show="isError">
      <strong>Error:</strong> City Not Found.
    </div>
  </div>
</template>

<script>
export default {
  props: ['forecast', 'isError'],
  data () {
    return {

    }
  },
  filters: {
    toCelcius(value) {
      value = value - 273.15
      return value.toFixed(2)
    },
    toKmHr(value) {
      value = value*3.6
      return value.toFixed(2)
    }
  }
}
</script>

<style scoped>
</style>
