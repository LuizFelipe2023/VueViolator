<script setup>
import { ref } from 'vue';

const props = defineProps({
  mostrarPopup: Function
});

let nome = ref('');
let email = ref('');
let telefone = ref('');
let assunto = ref('');
let descricao = ref('');

function submitForm() {
    if (!nome.value || !email.value || !telefone.value || !assunto.value || !descricao.value) {
        props.mostrarPopup("Por favor, preencha todos os campos", "erro");
        return;
    }

    let contato = {
        nome: nome.value,
        email: email.value,
        telefone: telefone.value,
        assunto: assunto.value,
        descricao: descricao.value
    };

    let contatos = JSON.parse(localStorage.getItem('contatos') || "[]");
    contatos.push(contato);
    localStorage.setItem('contatos', JSON.stringify(contatos));

    props.mostrarPopup("Formulário salvo com sucesso!", "sucesso");

    nome.value = '';
    email.value = '';
    telefone.value = '';
    assunto.value = '';
    descricao.value = '';
}
</script>

<template>
    <footer id="contato">
        <h2>Contato</h2>
        <div class="card-form">
            <form id="contact-form" @submit.prevent="submitForm">
                <div class="form-group">
                    <label for="nome">Nome:</label>
                    <input type="text" id="nome" v-model="nome" required>
                    <div class="error-message">Por favor, insira seu nome</div>
                </div>

                <div class="form-group">
                    <label for="email">Email:</label>
                    <input type="email" id="email" v-model="email" required>
                    <div class="error-message">Por favor, insira um email válido</div>
                </div>

                <div class="form-group">
                    <label for="telefone">Telefone:</label>
                    <input type="tel" id="telefone" v-model="telefone">
                </div>

                <div class="form-group">
                    <label for="assunto">Assunto:</label>
                    <input type="text" id="assunto" v-model="assunto" required>
                    <div class="error-message">Por favor, insira um assunto</div>
                </div>

                <div class="form-group">
                    <label for="descricao">Mensagem:</label>
                    <textarea id="descricao" rows="4" v-model="descricao" required></textarea>
                    <div class="error-message">Por favor, insira uma mensagem</div>
                </div>

                <button type="submit" class="btn" id="submit-btn">Enviar</button>
            </form>
        </div>

        <div class="socials">
            <a href="https://www.instagram.com/violatorthrash/">Instagram</a>
            <a href="https://www.youtube.com/watch?v=P5w_iarT_P8&list=PLMww4jbRqyryb9IydWdN6-OEIuu8GmEU4">YouTube</a>
            <a href="https://open.spotify.com/intl-pt/artist/0lFI9B2QSbFVqS6gAZzg1a?si=8u5WZp0ZQv-FUOPuyrUsSA&utm_medium=share&utm_source=linktree">Spotify</a>
            <a href="https://violatorthrash.bandcamp.com/album/unholy-retribution">Bandcamp</a>
        </div>
        <p>&copy; 2025 Violator. Todos os direitos reservados.</p>
    </footer>
</template>
