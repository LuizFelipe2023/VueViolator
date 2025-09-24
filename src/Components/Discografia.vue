<script setup>
import { ref, onMounted, nextTick, onBeforeUnmount } from "vue";

const track = ref(null);
const currentIndex = ref(0);
let slideWidth = 0;
let maxIndex = 0;

const slides = ref([]);

function updateCarousel() {
    track.value.style.transform = `translateX(-${currentIndex.value * slideWidth}px)`;
}

function nextSlide() {
    if (currentIndex.value < maxIndex) {
        currentIndex.value++;
        updateCarousel();
    }
}

function prevSlide() {
    if (currentIndex.value > 0) {
        currentIndex.value--;
        updateCarousel();
    }
}

function calcularMaxIndex() {
    if (!track.value) return;

    slides.value = Array.from(track.value.children);
    if (slides.value.length === 0) return;

    const gap = 20;
    slideWidth = slides.value[0].getBoundingClientRect().width + gap;

    const containerWidth = track.value.parentElement.offsetWidth;
    const visibleSlides = Math.floor(containerWidth / slideWidth);

    maxIndex = slides.value.length - visibleSlides;
    if (maxIndex < 0) maxIndex = 0;

    if (currentIndex.value > maxIndex) {
        currentIndex.value = maxIndex;
        updateCarousel();
    }
}

onMounted(async () => {
    await nextTick();
    calcularMaxIndex();
    window.addEventListener("resize", calcularMaxIndex);
});

onBeforeUnmount(() => {
    window.removeEventListener("resize", calcularMaxIndex);
});

const albums = [
    { link: "https://open.spotify.com/intl-pt/album/1TH5k2rVx1vAZb4YchmcbA", img: "/imgs/Chemical.jpg", alt: "Álbum 1" },
    { link: "https://open.spotify.com/intl-pt/album/2zxbDb9cnixcoAoNtPshHx", img: "/imgs/annihilation.jpg", alt: "Álbum 2" },
    { link: "https://open.spotify.com/intl-pt/album/69jW9XIFPGfqaNXmb8XXQz", img: "/imgs/Scenarios.jpg", alt: "Álbum 3" },
    { link: "https://open.spotify.com/intl-pt/album/49jf5Qqvx0ER8IED8Nj7Wq", img: "/imgs/Violator.png", alt: "Álbum 4" }
];
</script>

<template>
    <section id="discografia">
        <h2 class="section-title">Discografia</h2>

        <div class="carousel">
            <button class="carousel-btn prev" @click="prevSlide">&#10094;</button>

            <div class="carousel-track-container">
                <ul class="carousel-track" ref="track">
                    <li class="carousel-slide" v-for="(album, index) in albums" :key="index">
                        <a :href="album.link" target="_blank">
                            <img :src="album.img" :alt="album.alt">
                        </a>
                    </li>
                </ul>
            </div>

            <button class="carousel-btn next" @click="nextSlide">&#10095;</button>
        </div>
    </section>
</template>
