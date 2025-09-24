<script setup>
import { ref, onMounted } from 'vue';

const scrolled = ref(false);
const menuOpen = ref(false);

onMounted(() => {
  window.addEventListener('scroll', () => {
    scrolled.value = window.scrollY > 50;
  });
});

function toggleMenu() {
  menuOpen.value = !menuOpen.value;
}
</script>

<template>
 <div :class="['navbar', { scrolled }]">
    <div class="navbar-container">
        <a href="#" class="navbar-logo">Violator</a>

        <button class="navbar-toggler" type="button" aria-label="Toggle navigation" @click="toggleMenu">
            <span class="toggler-icon"></span>
            <span class="toggler-icon"></span>
            <span class="toggler-icon"></span>
        </button>

        <ul :class="['navbar-menu', { show: menuOpen }]">
            <li class="navbar-item"><a href="#hero" class="navbar-link">Início</a></li>
            <li class="navbar-item"><a href="#sobre" class="navbar-link">Sobre</a></li>
            <li class="navbar-item"><a href="#discografia" class="navbar-link">Discografia</a></li>
            <li class="navbar-item"><a href="#shows" class="navbar-link">Shows</a></li>
            <li class="navbar-item"><a href="#contato" class="navbar-link">Contato</a></li>
        </ul>
    </div>
</div>
</template>
