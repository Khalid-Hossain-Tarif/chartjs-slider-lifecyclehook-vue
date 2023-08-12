<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const fullImage = ref(
  'https://images.pexels.com/photos/5604097/pexels-photo-5604097.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1'
);
const activeImageIndex = ref(0);

const images = [
  {
    full: 'https://images.pexels.com/photos/5604097/pexels-photo-5604097.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    thumb:
      'https://images.pexels.com/photos/5604097/pexels-photo-5604097.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    name: 'slider 1',
  },
  {
    full: 'https://images.pexels.com/photos/5253109/pexels-photo-5253109.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    thumb:
      'https://images.pexels.com/photos/5253109/pexels-photo-5253109.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    name: 'slider 2',
  },
  {
    full: 'https://images.pexels.com/photos/4827896/pexels-photo-4827896.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    thumb:
      'https://images.pexels.com/photos/4827896/pexels-photo-4827896.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    name: 'slider 3',
  },
  {
    full: 'https://images.pexels.com/photos/7141188/pexels-photo-7141188.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    thumb:
      'https://images.pexels.com/photos/7141188/pexels-photo-7141188.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    name: 'slider 4',
  },
  {
    full: 'https://images.pexels.com/photos/7141191/pexels-photo-7141191.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    thumb:
      'https://images.pexels.com/photos/7141191/pexels-photo-7141191.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    name: 'slider 5',
  },
];

const setFullImage = (image, index) => {
  fullImage.value = image.full;
  activeImageIndex.value = index;
};

const autoSlide = () => {
  if (activeImageIndex.value === images.length - 1) {
    activeImageIndex.value = 0;
  } else {
    activeImageIndex.value = activeImageIndex.value + 1;
  }
  fullImage.value = images[activeImageIndex.value].full;
};

const slideInterval = setInterval(autoSlide, 3000);

onMounted(() => {
  fullImage.value = images[activeImageIndex.value].full;
});

onBeforeUnmount(() => {
  clearInterval(slideInterval);
});
</script>

<template>
  <section class="relative h-[350px] sm:h-screen">
    <div class="h-full">
      <img
        class="h-full w-full object-cover object-right-bottom sm:object-center"
        :src="fullImage"
      />
    </div>

    <!-- Thumbs -->
    <div
      class="
        flex
        gap-2
        sm:gap-4
        absolute
        bottom-10
        left-1/2
        -translate-x-1/2
        overflow-hidden
      "
    >
      <img
        class="
          w-8
          sm:w-16
          h-8
          sm:h-16
          rounded-full
          shadow-xl
          cursor-pointer
          border-2
          sm:border-4
          border-white
          hover:brightness-100
          transition
          duration-300
        "
        :class="index === activeImageIndex ? 'brightness-100' : 'brightness-50'"
        :src="image.thumb"
        @click="setFullImage(image, index)"
        v-for="(image, index) in images"
        :key="index"
      />
    </div>
  </section>
</template>