<template>
  <div class="gallery">
    <div v-for="(image, index) in images" :key="index" class="gallery-item">
      <img :src="image.url" :alt="image.title" @click="openImage(index)" />
    </div>

    <div v-if="selectedImageIndex !== null" class="modal" @click="closeImage">
      <img :src="images[selectedImageIndex].link" :alt="images[selectedImageIndex].title" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
      selectedImageIndex: null,
    };
  },
  methods: {
    fetchImages() {
      fetch('https://backlogbok.onrender.com/api/v1/profiles/1')
          .then(response => response.json())
          .then(data => {
            this.images = data.images;
          })
          .catch(error => console.error('Error fetching images:', error));
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
.gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.gallery-item {
  width: 200px;
  cursor: pointer;
}

.gallery-item img {
  width: 100%;
  height: auto;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal img {
  max-width: 90%;
  max-height: 90%;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}
</style>
