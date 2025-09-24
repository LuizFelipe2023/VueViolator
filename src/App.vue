<script setup>
import { ref } from "vue";

import Navbar from './Components/Navbar.vue';
import Banner from './Components/Banner.vue';
import Sobre from './Components/Sobre.vue';
import Discografia from './Components/Discografia.vue';
import Shows from './Components/Shows.vue';
import Footer from './Components/Footer.vue';
import PopupMensagem from './Components/PopupMensagem.vue';
import SpotifyPlayer from "./Components/SpotifyPlayer.vue";

const mensagem = ref("");
const tipoMensagem = ref("");

function mostrarPopup(msg, tipo = "sucesso") {
  mensagem.value = msg;
  tipoMensagem.value = tipo;
}
</script>

<template>
  <Navbar />
  <PopupMensagem :mensagem="mensagem" :tipo="tipoMensagem" />
  <SpotifyPlayer></SpotifyPlayer>
  <Banner />
  <Sobre />
  <Discografia />
  <Shows />
  <Footer :mostrarPopup="mostrarPopup" />
</template>
