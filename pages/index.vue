<template>
  <div v-if="loading" class="text-center mt-36">
    Carregando...
  </div>
  <div v-else class="container mx-auto p-4">
    <h1 class="text-3xl font-bold mb-4">Catálogo de Jogos HTML5</h1>
    <div>
      <div v-for="(games, category) in categorizedGames" :key="category" class="mb-8">
        <div class="flex justify-between items-center mb-2">
          <h2 class="text-2xl font-semibold mb-2">{{ category }}</h2>
          <button @click="goToCategory(category)"
            class="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-700 transition duration-200">
            Ver mais
          </button>
        </div>
        <div class="flex overflow-x-auto space-x-4 pb-4">
          <div v-for="game in games.slice(0, 10)" :key="game.id"
            class="game-card p-4 border rounded-lg shadow-lg w-60 flex-shrink-0 flex flex-col">
            <h3 class="text-md font-semibold mb-2 truncate">{{ game.title }}</h3>
            <img :src="game.thumb" :alt="game.title" class="w-full h-40 object-cover mb-2 rounded-lg" />
            <p class="text-gray-700 mb-2"><strong>Categoria:</strong> {{ game.category }}</p>
            <div class="mt-auto">
              <button @click="goToGame(game)"
                class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700 transition duration-200 w-full">
                Jogar
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';

const router = useRouter();
const games = ref([]);
const categorizedGames = ref({});
const loading = ref(true);

const categorizeGames = (gamesList) => {
  const categories = {};
  gamesList.forEach((game) => {
    if (!categories[game.category]) {
      categories[game.category] = [];
    }
    categories[game.category].push(game);
  });
  categorizedGames.value = categories;
};

const getGames = async () => {
  try {
    console.log('Fetching games...');
    const response = await axios.get('https://gamemonetize.com/feed.php?format=0&page=1');
    console.log('Games fetched:', response.data);
    games.value = response.data;
    categorizeGames(response.data);
  } catch (error) {
    console.error('Erro ao buscar jogos:', error);
  } finally {
    loading.value = false;
  }
};

const goToGame = (game) => {
  router.push({ path: `/game/${game.id}`, query: { title: game.title, url: game.url, thumbnail: game.thumb, category: game.category, description: game.description, instructions: game.instructions } });
};

const goToCategory = (category) => {
  router.push({ path: `/category/${category}` });
};

onMounted(() => {
  getGames();
});
</script>

<style scoped>
img {
  display: block;
  max-width: 100%;
  height: auto;
}
</style>
