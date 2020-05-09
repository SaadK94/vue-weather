<template>
  <div class="container">
    <app-header></app-header>
    <br />
    <div class="row d-flex justify-content-center h-100">
      <div class="col-sm-8">
        <div class="input-group shadow-sm">
          <input
            type="text"
            class="form-control bg-white rounded"
            placeholder="Enter city..."
            v-model="search"
            @keypress.enter="buttonPressed(units)"
          />
          <div class="btn-group btn-group-toggle" data-toggle="buttons">
            <label class="btn btn-outline-primary" :class="{ active: isActive }">
              <input
                type="radio"
                name="unit"
                value="metric"
                v-model="units"
                @click="getWeather('metric'); isActive=!isActive"
              /> °C
            </label>
            <label class="btn btn-outline-primary" :class="{ active: !isActive }">
              <input
                type="radio"
                name="unit"
                value="imperial"
                v-model="units"
                @click="getWeather('imperial'); isActive=!isActive"
              /> °F
            </label>
          </div>
        </div>
        <br />
        <app-weather-card
          :weather="weather"
          :unitType="unitType"
          :cityPhoto="cityPhoto"
          v-if="!isEmpty"
        ></app-weather-card>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import WeatherCard from "./components/WeatherCard.vue";
import axios from "axios";

export default {
  data() {
    return {
      search: "",
      cityPhoto: "",
      weatherKey: "68eef01e882d85af98d8994adc7e829f",
      unsplashKey: "F2qE0ZhelKvu9jdtFZiGko60P9GD3L3Y4piH9FAoBGg",
      weather: {},
      units: "metric",
      isActive: true
    };
  },
  methods: {
    buttonPressed(units) {
      this.getWeather(units);
      this.getPic();
    },
    getWeather(units) {
      if (!this.search) return;
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.search}&units=${units}&appid=${this.weatherKey}`
        )
        .then(res => {
          this.weather = res.data;
        })
        .catch(err => {
          alert("Please search for a valid city");
        });
    },
    getPic() {
      if (!this.search || !this.isEmpty) return;
      axios
        .get(
          `https://api.unsplash.com/search/photos?query=${this.search}&client_id=${this.unsplashKey}`
        )
        .then(res => {
          this.cityPhoto = res.data.results[0].urls.regular;
        });
    }
  },
  computed: {
    isEmpty() {
      return Object.entries(this.weather).length === 0;
    },
    unitType() {
      if (this.units === "metric") {
        return "°C";
      } else {
        return "°F";
      }
    }
  },
  components: {
    appHeader: Header,
    appWeatherCard: WeatherCard
  }
};
</script>

<style>
.card-img-bottom {
  width: 100%;
  height: 25vw;
  object-fit: cover;
}
</style>
