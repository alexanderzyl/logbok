<template>
  <div id="app">
    <h1>Vehicles</h1>
    <Galleria :value="images" :numVisible="5" :responsiveOptions="responsiveOptions" containerStyle="max-width: 640px">
      <template #item="slotProps">
        <img :src="slotProps.item.itemImageSrc" :alt="slotProps.item.alt" style="width: 100%" />
      </template>
      <template #thumbnail="slotProps">
        <img :src="slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" class="thumbnail" />
      </template>
    </Galleria>
<!--    <h1>Map</h1>-->
<!--    <MapBox/>-->
  </div>
</template>

<script>
// import MapBox from './components/Map.vue';
import Galleria from 'primevue/galleria';

export default {
  name: 'App',
  components: {
    // MapBox,
    Galleria,
  },
  data() {
    return {
      images: [],
      responsiveOptions: [
        {
          breakpoint: '1024px',
          numVisible: 3,
          numScroll: 3
        },
        {
          breakpoint: '600px',
          numVisible: 2,
          numScroll: 2
        },
        {
          breakpoint: '480px',
          numVisible: 1,
          numScroll: 1
        }
      ]
    };
  },
  methods: {
    fetchImages() {
      fetch('https://backlogbok.onrender.com/api/v1/profiles/2')
          .then(response => response.json())
          .then(data => {
            // For demonstration purposes, we only use the first 10 images
            const fetchedImages = this.shuffleArray(data.images).slice(0, 10);
            this.images = fetchedImages.map(img => ({
              itemImageSrc: img.url,
              thumbnailImageSrc: img.url,
              alt: 'Image Alt Text' // Replace this with actual alt text if available
            }));
          })
          .catch(error => console.error('Error fetching images:', error));
    },
    shuffleArray(array) {
      let i = array.length - 1;
      for (; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    },
    openImage(index) {
      this.selectedImageIndex = index;
    },
    closeImage() {
      this.selectedImageIndex = null;
    },
  },
  mounted() {
    this.fetchImages();
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
.thumbnail {
  max-width: 100px; /* adjust as per your requirement */
  max-height: 100px; /* adjust as per your requirement */
}
</style>
