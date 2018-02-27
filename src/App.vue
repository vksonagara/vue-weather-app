<template>
  <div id="weather-app">
    <weather-widget v-on:getWeatherInfo="getWeatherInfo($event)"></weather-widget>
    <weather-info v-bind:forecast="forecast" v-bind:isError="isError"></weather-info>
  </div>
</template>

<script>
import weatherWidget from './components/weatherWidget.vue'
import weatherInfoWidget from './components/weatherInfoWidget.vue'

export default {
  components: {
    'weather-widget': weatherWidget,
    'weather-info': weatherInfoWidget
  },
  data () {
    return {
      position: {
        lat: null,
        long: null
      },
      forecast: {
        cityName: '',
        temperature: null,
        windSpeed: null,
        main: '',
        description: ''
      },
      isError: false
    }
  },
  created() {
    navigator.geolocation.getCurrentPosition((position) => {
      this.position.lat = Math.round(position.coords.latitude)
      this.position.long = Math.round(position.coords.longitude)
      this.$http.get('http://api.openweathermap.org/data/2.5/weather?lat=' + this.position.lat +'&lon=' + this.position.long + '&appid=6096f17952cdad7888f24c9560ffbb3c')
      .then(response => {
        this.forecast.cityName = response.body.name
        this.forecast.temperature = response.body.main.temp
        this.forecast.windSpeed = response.body.wind.speed
        this.forecast.main = response.body.weather[0].main
        this.forecast.description = response.body.weather[0].description
        this.isError = false
      })
    }, () => {
      console.log('Could not get position');
    })
  },
  methods: {
    getWeatherInfo(cityName) {
      this.$http.get('http://api.openweathermap.org/data/2.5/weather?q=' + cityName + '&appid=6096f17952cdad7888f24c9560ffbb3c')
      .then(response => {
        this.forecast.cityName = response.body.name
        this.forecast.temperature = response.body.main.temp
        this.forecast.windSpeed = response.body.wind.speed
        this.forecast.main = response.body.weather[0].main
        this.forecast.description = response.body.weather[0].description
        this.isError = false
      }, response => {
        this.isError = true
      })
    }
  }
}
</script>

<style scoped>
#weather-app {
  width: 100%;
  background: url('./assets/light-background.jpg') no-repeat;
  height: 100vh;
  padding-top: 20vh;
}
</style>
