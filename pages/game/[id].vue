<template>
    <div v-if="loading" class="text-center mt-36">
        Carregando...
    </div>
    <div v-else class="container mx-auto p-4">
        <div class="flex mb-4">
            <div class="w-64">
                <button @click="goBack"
                    class="back-button bg-blue-500 text-white w-full py-2 rounded hover:bg-blue-700 transition duration-200 mb-4">
                    ← Voltar
                </button>
                <div class="advertisement">
                    <!-- Coloque seus anúncios aqui -->
                    <img src="https://via.placeholder.com/300x250" alt="Ad" class="mb-4" />
                    <img src="https://via.placeholder.com/300x250" alt="Ad" class="mb-4" />
                    <img src="https://via.placeholder.com/300x250" alt="Ad" class="mb-4" />
                </div>
            </div>
            <div class="flex-grow ml-4">
                <h1 class="text-3xl font-bold mb-4">{{ title }}</h1>
                <img :src="thumbnail" :alt="title" class="w-full h-auto mb-4 rounded-lg" />
                <p class="text-gray-700 mb-2"><strong>Categoria:</strong> {{ category }}</p>
                <p class="text-gray-700 mb-2"><strong>Descrição:</strong> {{ description }}</p>
                <p class="text-gray-700 mb-4"><strong>Instruções:</strong> {{ instructions }}</p>
                <iframe :src="url" :width="width" :height="height" scrolling="none" frameborder="0"
                    class="w-full rounded-lg"></iframe>
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
});

const goBack = () => {
    router.push('/');
};
</script>

<style scoped>
.back-button {
    transition: transform 0.2s;
}

.back-button:hover {
    transform: scale(1.05);
}
</style>