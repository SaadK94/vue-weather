<template>
  <div class="card border-info mb-3 shadow-lg mh-100">
    <h5 class="card-header">{{ weather.name }}, {{ weather.sys.country }}</h5>
    <div class="card-body">
      <h5 class="card-title">Temperature: {{ Math.round(weather.main.temp) }}{{ unitType }}</h5>
      <p class="card-text">Feels like {{ Math.round(weather.main.feels_like) }}{{ unitType }}</p>
      <p class="card-text">{{ weather.weather[0].main }}</p>
    </div>
    <img :src="cityPhoto" class="card-img-bottom img-fluid mw-100" />
  </div>
</template>

<script>
export default {
  props: ["weather", "unitType", "cityPhoto"]
};
</script>