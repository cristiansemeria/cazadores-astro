<script setup>
import { ref } from 'vue'

// Imagenes a mostrar
const props = defineProps({
  images: {
    type: Array,
    default: () => [],
  },
});

// Estado del modal
const isModalOpen = ref(false);
const modalSrc = ref('');

function openModal(src) {
  modalSrc.value = src;
  isModalOpen.value = true;
  document.body.style.overflow = 'hidden';
}

function closeModal() {
  isModalOpen.value = false;
  modalSrc.value = '';
  document.body.style.overflow = '';
}
</script>

<template>
  <div class="grid grid-cols-1 xl:grid-cols-2 gap-5 mx-5 xl:mx-0">
    <div v-for="(img, idx) in images" :key="idx" class="w-full h-full">
      <img
          :src="img.src"
          :alt="img.alt"
          class="cursor-pointer object-cover object-top rounded-xl w-full h-full"
          @click="openModal(img.src)"
      />
    </div>
  </div>

  <!-- Modal -->
  <div
      v-if="isModalOpen"
      v-for="(img) in images"
      class="fixed inset-0 bg-black/90 flex items-center justify-center overflow-hidden z-5"
      @click="closeModal"
  >
    <img
        :src="modalSrc"
        :alt="img.alt"
        class="max-w-full max-h-full px-5 xl:px-0"
    />
  </div>
</template>

<style scoped>
/* Opcional: transiciones suaves */
img {
  transition: transform 0.3s ease;
}
img:hover {
  transform: scale(1.02);
}
</style>