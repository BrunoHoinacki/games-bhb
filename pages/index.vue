<template>
  <div v-if="loading" class="text-center mt-48">
    <LoadingSpinner />
    <p class="mt-4">Carregando...</p>
  </div>
  <div v-else class="container mx-auto p-4">
    <div class="flex justify-center mb-8">
      <div class="bg-gradient-to-r from-teal-700 via-teal-500 to-teal-700 p-6 rounded-lg shadow-lg text-center">
        <h1 class="text-3xl md:text-5xl font-bold mb-2">
          <span v-for="(letter, index) in letters" :key="index" :class="`letter letter-${index}`">{{ letter }}</span>
        </h1>
        <p class="text-white text-base md:text-xl">Bem-vindo ao Joga-Aqui.com!</p>
      </div>
    </div>
    <div>
      <div v-for="(games, category) in categorizedGames" :key="category" class="mb-12">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-3xl font-bold text-white">{{ category }}</h2>
          <button @click="goToCategory(category)"
            class="bg-yellow-500 text-black px-6 py-2 rounded-full hover:bg-yellow-600 transition duration-200">
            Ver mais
          </button>
        </div>
        <div class="flex overflow-x-auto space-x-6 pb-6">
          <div v-for="game in games.slice(0, 10)" :key="game.id"
            class="p-4 border rounded-lg shadow-lg shadow-gray-200/50 w-60 flex-shrink-0 flex flex-col bg-white">
            <h3 class="text-lg font-semibold mb-2 truncate text-yellow-500">{{ game.title }}</h3>
            <img :src="game.thumb" :alt="game.title" class="w-full h-40 object-cover mb-2 rounded-lg" />
            <p class="text-yellow-500 mb-2"><strong>Categoria:</strong> {{ game.category }}</p>
            <div class="mt-auto">
              <button @click="goToGame(game)"
                class="bg-yellow-500 text-white px-4 py-2 rounded-full hover:bg-yellow-600 transition duration-200 w-full">
                <i class="fas fa-gamepad mr-2"></i> Jogar
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

const title = "Joga-Aqui.com";
const letters = title.split("");

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
@keyframes colorChange {

  0%,
  100% {
    color: #f59e0b;
  }

  16% {
    color: #ef4444;
  }

  32% {
    color: #10b981;
  }

  48% {
    color: #3b82f6;
  }

  64% {
    color: #8b5cf6;
  }

  80% {
    color: #ec4899;
  }
}

.letter {
  animation: colorChange 3s infinite;
  display: inline-block;
  transition: transform 0.3s;
}

.letter:hover {
  transform: scale(1.2);
}
</style>
