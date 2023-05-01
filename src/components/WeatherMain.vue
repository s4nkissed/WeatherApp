<template>
  <div>
    <div class="main">
      <div class="container">
        <div v-if="weather" class="content">
          <div class="header">
            <h1>{{ weather.name }}</h1>
            <h3>{{ new Date().toLocaleString() }}</h3>
          </div>
          <div class="temp" v-bind:class="stateWeather">
            <h2> {{ Math.round(weather.main.temp) }}&deg;</h2>
          </div>
          <div class="state">
            <h3> {{ weather.weather[0].main }} </h3>
            <h3> {{ Math.round(weather.wind.speed) }}m/s </h3>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>


const COLD = -10
const WARM = 24
const STATE_WEATHER = {
  cold: {
    value: 'cold',
    compare: (value) => value <= COLD,
  },
  warm: {
    value: 'warm',
    compare: (value) => value >= WARM,
  }
}

export default {
  name: 'WeatherMain',
  props: {
    weather: {
      type: Object,
      require: true
    }
  },
  computed: {
    stateWeather() {
      const [res] = Object.values(STATE_WEATHER).filter((value) => {
        return value.compare(this.weather.main.temp)
      })
      return res?.value || null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: monospace;
}


.main {
  min-height: 100vh;
  padding: 25px;
}

.container {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

.container .search-bar {
  display: block;
  width: 50%;
  padding: 16px;

  color: #313131;
  font-size: 20px;
  border: none;
  appearance: none;
  outline: none;
  background-color: rgba(132, 186, 217, 0.75);
  border-radius: 16px;
  transition: 0.4s;
  box-shadow: 3px 3px rgba(0, 0, 0, 0.25);
}

.container .search-bar:focus {
  box-shadow: 0 0 16px;
  background-color: white;
}

.content {
  min-width: 300px;
}

.header, .state, .temp {
  color: aliceblue;
}

.header {
  margin: 5px;
  align-items: center;
  justify-content: space-between;
  color: aliceblue;
  font-style: italic;
  text-shadow: 3px 3px rgba(0, 0, 0, 0.25);
  text-align: center;
}

.state {
  margin: 5px;
  display: flex;
  justify-content: space-between;
  color: aliceblue;
  font-size: 24px;
  font-style: italic;
  text-shadow: 3px 3px rgba(0, 0, 0, 0.25);
  text-align: center;
}

.temp {
  display: flex;
  justify-content: center;

  font-size: 100px;
  font-weight: 1000;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);

  background-image: linear-gradient(to bottom, rgba(172, 218, 67, 0.35), rgba(207, 218, 34, 0.75));
  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  padding: 5px;
}

.temp.warm {
  font-size: 100px;
  font-weight: 1000;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);

  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  padding: 5px;
  background-image: linear-gradient(to bottom, rgba(248, 8, 8, 0.35), rgba(246, 6, 6, 0.75));
}

.temp.cold {
  font-size: 100px;
  font-weight: 1000;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);

  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  padding: 5px;
  background-image: linear-gradient(to bottom, rgb(0, 185, 204, 0.35), rgb(1, 140, 209, 0.75));
}
</style>