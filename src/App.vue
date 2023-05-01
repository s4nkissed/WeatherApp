<template>
  <div class="main-page" :style="{backgroundImage: `url(${background})`}">
    <div class="container">
      <CountrySearch @update:model-value="getApi" v-model="city"/>
      <WeatherMain :weather="weather"/>
    </div>
  </div>

</template>

<script>
import WeatherMain from "@/components/WeatherMain.vue";
import CountrySearch from "@/components/CountrySearch.vue";
import axios from "axios";
import {throttle} from "@/utils";
import weatherState from "@/assets/img/weather.state";



export default {
  name: 'App',
  components: {
    WeatherMain,
    CountrySearch
  },

  data: () => ({
    weather: null,
    city: '',
    api_key: '16ebfd878bcccd07be6d2270e84b46e2',
    current_day: '',
    state_weather: false
  }),

  mounted: async function () {
    this.getApi()
  },

  methods: {
    getApi: throttle(async function () {

      const {data} = await axios.get(
          `https://api.openweathermap.org/data/2.5/weather?units=metric&q=${this.city}&appid=${this.api_key}`
      )
      this.weather = data
      console.log(this.weather)
    }, 1000),
  },

  computed: {
    background() {
      const main = this.weather?.weather[0].main
      if (main) {
        return weatherState[main]
      }
      return weatherState.Sunny
    },
  },

}
</script>

<style>

.main-page {
  background-size: cover;
  transition: 1s;
  backdrop-filter: blur(3px);
}






</style>
