<template>
  <div class="carousel">
    <div class="carousel-inner">
      <div v-for="(image, index) in images" :key="index" :class="['carousel-slide', { active: index === currentIndex }]">
        <img :src="image" alt="Carousel Image" />
      </div>
    </div>
    <button @click="prevSlide" class="carousel-button prev">Previous</button>
    <button @click="nextSlide" class="carousel-button next">Next</button>
  </div>
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from 'vue';

export default {
  name: 'Carousel',
  setup() {
    const images = [
      'https://pixabay.com/get/ge2d58597b8429b7bbb196c4ac46403808427ef03d1f4cd4a8e7829775c1a83ade323e767d9c2f4830b26e0b70af8d674f047c97e81dae2532efcac2970b54054_1280.jpg',
      'https://pixabay.com/get/g9c41de6a52bdf7127cdd594afe3d7e3632fa99005d78f091ca7355563a56dd732b87e8ffd1a10a21a6e91549d04f2a6f845113c93f770dc121ace1908a3d9033_1280.jpg',
      'https://pixabay.com/get/g146681436aa910ecc4deb4ab45883c204a8e73d22c5c11eb6f7307cf5ab84399f3be97308c9e4d3f5183b39300657a1dcc1deee0734ad5fa491f5a244069e3ce_1280.jpg',
      // Add more image URLs here
    ];

    const currentIndex = ref(0);

    const prevSlide = () => {
      currentIndex.value = (currentIndex.value - 1 + images.length) % images.length;
    };

    const nextSlide = () => {
      currentIndex.value = (currentIndex.value + 1) % images.length;
    };

    const intervalId = setInterval(nextSlide, 3000); // Auto advance every 3 seconds

    onMounted(() => {
      // Initialization code here
    });

    onBeforeUnmount(() => {
      clearInterval(intervalId); // Clear the interval to clean up
    });

    return {
      images,
      currentIndex,
      prevSlide,
      nextSlide,
    };
  },
};
</script>

<style scoped>
.carousel {
  position: relative;
  width: 100%;
  overflow: hidden;
}

.carousel-inner {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-slide {
  flex: 0 0 100%;
}

.active {
  transform: translateX(0);
}

.carousel-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding: 10px 15px;
  border: none;
  background-color: #333;
  color: #fff;
  cursor: pointer;
}

.prev {
  left: 0;
}

.next {
  right: 0;
}
</style>
