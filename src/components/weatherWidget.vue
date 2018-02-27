<template>
  <div class="container">
    <form v-on:submit.prevent="getWeather">
      <div class="form-group">
        <input type="text" name="cityName" placeholder="eg. London" class="form-control form-control-sm" v-model="cityName" autocomplete="off">
      </div>
      <div class="form-group">
        <button type="button" class="btn btn-primary btn-sm" v-on:click.prevent="getWeather">Search</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      cityName: ''
    }
  },
  methods: {
    getWeather() {
      this.$emit('getWeatherInfo', this.cityName)
    }
  }
}
</script>

<style scoped>
</style>
