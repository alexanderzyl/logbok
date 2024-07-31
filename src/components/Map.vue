<template>
  <div id="map" :style="{ width: '100%', height: '500px' }"></div>
</template>

<script>
import mapboxgl from 'mapbox-gl';

export default {
  name: 'MapBox',
  mounted() {
    mapboxgl.accessToken = 'pk.eyJ1IjoiYXp5bHNvZnQiLCJhIjoiY2x6NzY3a3ExMDYxbjJpczVyZGxzd2R6biJ9.3Co395qaKUdX4xlZieOj5Q';
    this.map = new mapboxgl.Map({
      container: 'map',
      style: 'mapbox://styles/mapbox/streets-v11',
      center: [5.47, 51.43], // starting position [lng, lat]
      zoom: 9, // starting zoom
    });
  },
};
</script>

<style>
#map {
  position: relative;
  width: 100%;
  height: 500px;
}
</style>
