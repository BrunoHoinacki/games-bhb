<template>
    <div v-if="loading" class="text-center mt-48">
        <LoadingSpinner />
        <p class="mt-4">Carregando...</p>
    </div>
    <div v-else class="container mx-auto p-4">
        <div class="flex flex-col md:flex-row mb-4">
            <div class="flex-grow md:mx-4">
                <h1 class="text-2xl md:text-3xl font-extrabold mb-4 text-yellow-500">{{ title }}</h1>
                <div class="flex flex-col md:flex-row mb-4">
                    <img :src="thumbnail" :alt="title" class="w-full md:w-1/3 h-auto mb-4 md:mb-0 rounded-lg md:mr-4" />
                    <div class="flex-grow">
                        <p class="text-white mb-2"><strong>Categoria:</strong> {{ category }}</p>
                        <p class="text-white mb-2"><strong>Descrição:</strong> {{ description }}</p>
                        <p class="text-white mb-4"><strong>Instruções:</strong> {{ instructions }}</p>
                    </div>
                </div>
                <div class="relative border-4 border-gray-300 rounded-lg">
                    <div class="relative" style="padding-top: 56.25%;">
                        <iframe ref="gameIframe" :src="url" frameborder="0" scrolling="no" allowfullscreen
                            class="absolute top-0 left-0 w-full h-full rounded-lg"></iframe>
                    </div>
                    <button @click="toggleFullscreen"
                        class="absolute bottom-4 right-4 bg-blue-500 text-white p-2 px-3 rounded-lg hover:bg-blue-700 transition duration-200">
                        <i
                            :class="isFullscreen ? 'fa-solid fa-down-left-and-up-right-to-center' : 'fa-solid fa-up-right-and-down-left-from-center'"></i>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
const title = ref('');
const url = ref('');
const thumbnail = ref('');
const category = ref('');
const description = ref('');
const instructions = ref('');
const width = ref('');
const height = ref('');
const loading = ref(true);
const gameIframe = ref(null);
const isFullscreen = ref(false);

onMounted(() => {
    title.value = route.query.title;
    url.value = route.query.url;
    thumbnail.value = route.query.thumbnail;
    category.value = route.query.category;
    description.value = route.query.description;
    instructions.value = route.query.instructions;
    width.value = route.query.width || "720";
    height.value = route.query.height || "1280";
    loading.value = false;

    document.addEventListener('fullscreenchange', () => {
        isFullscreen.value = !!document.fullscreenElement;
    });
    document.addEventListener('webkitfullscreenchange', () => {
        isFullscreen.value = !!document.webkitFullscreenElement;
    });
    document.addEventListener('mozfullscreenchange', () => {
        isFullscreen.value = !!document.mozFullScreenElement;
    });
    document.addEventListener('msfullscreenchange', () => {
        isFullscreen.value = !!document.msFullscreenElement;
    });
});

const goBack = () => {
    router.push('/');
};

const toggleFullscreen = () => {
    if (!isFullscreen.value) {
        if (gameIframe.value.requestFullscreen) {
            gameIframe.value.requestFullscreen();
        } else if (gameIframe.value.mozRequestFullScreen) { // Firefox
            gameIframe.value.mozRequestFullScreen();
        } else if (gameIframe.value.webkitRequestFullscreen) { // Chrome, Safari and Opera
            gameIframe.value.webkitRequestFullscreen();
        } else if (gameIframe.value.msRequestFullscreen) { // IE/Edge
            gameIframe.value.msRequestFullscreen();
        }
    } else {
        if (document.exitFullscreen) {
            document.exitFullscreen();
        } else if (document.mozCancelFullScreen) { // Firefox
            document.mozCancelFullScreen();
        } else if (document.webkitExitFullscreen) { // Chrome, Safari and Opera
            document.webkitExitFullscreen();
        } else if (document.msExitFullscreen) { // IE/Edge
            document.msExitFullscreen();
        }
    }
};
</script>

<style scoped>
/* Adicione seus estilos personalizados aqui */
</style>
