<template>
  <div class="row d-flex justify-content-center h-100">
    <div class="col-sm-8">
      <div class="input-group shadow-sm">
        <input
          type="text"
          class="form-control bg-white rounded"
          placeholder="Search..."
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
    </div>
  </div>
</template>

<script>
export default {
  props: []
};
</script>