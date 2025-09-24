<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  mensagem: String,
  tipo: {
    type: String,
    default: "info"
  },
  duracao: {
    type: Number,
    default: 3000
  }
});

const visivel = ref(false);

watch(() => props.mensagem, (novaMensagem) => {
  if (novaMensagem) {
    visivel.value = true;
    setTimeout(() => visivel.value = false, props.duracao);
  }
});
</script>

<template>
  <div v-if="visivel" :class="['popup-mensagem', tipo]">
    {{ mensagem }}
  </div>
</template>