<template>
    <div v-if="loading" class="text-center mt-48">
        <LoadingSpinner />
        <p class="mt-4">Carregando...</p>
    </div>
    <div v-else class="container mx-auto p-4">
        <div class="flex justify-between items-center mb-4">
            <button @click="goBackHome"
                class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700 transition duration-200 transform hover:scale-105">
                ← Voltar para Home
            </button>
            <h1 class="text-5xl font-bold text-gray-800">{{ category }} - Todos os Jogos</h1>
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
            <div v-for="game in games" :key="game.id"
                class="p-4 border rounded-lg shadow-lg transform transition-transform duration-200 hover:scale-105 bg-white">
                <h2 class="text-2xl font-semibold mb-2 text-gray-800">{{ game.title }}</h2>
                <img :src="game.thumb" :alt="game.title" class="w-full h-40 object-cover mb-2 rounded-lg" />
                <p class="text-gray-700 mb-2"><strong>Categoria:</strong> {{ game.category }}</p>
                <button @click="goToGame(game)"
                    class="bg-yellow-500 text-white px-4 py-2 rounded-full hover:bg-yellow-600 transition duration-200 w-full">
                    Jogar
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import axios from 'axios';

const route = useRoute();
const router = useRouter();
const category = ref(route.params.category);
const games = ref([]);
const loading = ref(true);

const getGames = async () => {
    try {
        console.log('Fetching games for category:', category.value);
        const response = await axios.get(`https://gamemonetize.com/feed.php?format=0&page=1`);
        console.log('Games fetched:', response.data);
        games.value = response.data.filter(game => game.category === category.value);
    } catch (error) {
        console.error('Erro ao buscar jogos:', error);
    } finally {
        loading.value = false;
    }
};

const goToGame = (game) => {
    router.push({ path: `/game/${game.id}`, query: { title: game.title, url: game.url, thumbnail: game.thumb, category: game.category, description: game.description, instructions: game.instructions } });
};

const goBackHome = () => {
    router.push('/');
};

onMounted(() => {
    getGames();
});
</script>

<style scoped>
/* Removido o CSS customizado em favor das classes utilitárias do Tailwind CSS */
</style>
