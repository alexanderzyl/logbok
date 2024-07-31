<template>
  <div id="app">
    <h1>Image Gallery</h1>
    <ImageGallery />
    <h1>Map</h1>
    <MapBox/>
  </div>
</template>

<script>
import MapBox from './components/Map.vue';
import ImageGallery from "@/components/ImageGallery.vue";

export default {
  name: 'App',
  components: {
    MapBox,
    ImageGallery,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
