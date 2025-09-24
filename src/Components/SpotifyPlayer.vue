<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const isPopupActive = ref(false);

function openPopup() {
  isPopupActive.value = true;
}

function closePopup() {
  isPopupActive.value = false;
}

function handleKeydown(e) {
  if (e.key === 'Escape') {
    closePopup();
  }
}

onMounted(() => {
  document.addEventListener('keydown', handleKeydown);
});

onBeforeUnmount(() => {
  document.removeEventListener('keydown', handleKeydown);
});
</script>

<template>
  <button class="spotify-popup-btn" @click="openPopup">
    🎵
  </button>

  <div :class="['spotify-popup', { active: isPopupActive }]">
    <div class="spotify-header">
      <h3>VIOLATOR - UNHOLY RETRIBUTION</h3>
      <button class="close-popup" @click="closePopup">X</button>
      <div class="blood-drip"></div>
    </div>

    <div class="spotify-player">
      <iframe
        src="https://open.spotify.com/embed/album/49jf5Qqvx0ER8IED8Nj7Wq?utm_source=generator&theme=0"
        allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
        loading="lazy"
      ></iframe>
    </div>
  </div>

  <div
    id="overlay"
    :class="{ active: isPopupActive }"
    @click="closePopup"
    class="overlay"
  ></div>
</template>
