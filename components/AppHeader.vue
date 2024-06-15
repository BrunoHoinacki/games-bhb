<template>
    <nav class="bg-teal-500 fixed w-full top-0 z-50 shadow-md bg-opacity-60 backdrop-blur border-b border-gray-400">
        <div class="container mx-auto flex justify-between items-center pt-2 px-4 pb-2">
            <a href="/" class="text-white text-xl font-bold">
                <img class="h-14 hover:scale-110 hover:duration-500 hover:bg-teal-500 rounded-lg" src="/public/images/logo-sem-fundo.png" alt="Logo">
            </a>
            <ul class="flex space-x-4">
                <li class="hover:bg-teal-500 rounded-lg p-1 hidden md:inline cursor-pointer"><a href="/" class="text-white"><i
                            class="fas fa-home"></i> Home</a></li>
                <li class="hover:bg-teal-500 rounded-lg p-1 hidden md:inline cursor-pointer"><a href="#" class="text-white"><i
                            class="fas fa-layer-group"></i> Games</a></li>
                <li @click="openChatModal" class="hover:bg-teal-500 rounded-lg p-1 hidden md:inline cursor-pointer"><a
                        href="#" class="text-white"><i class="fas fa-comments"></i> Chat</a></li>
                <li class="hover:bg-teal-500 rounded-lg p-1 md:hidden"><a href="/" class="text-white"><i
                            class="fas fa-home"></i></a></li>
                <li class="hover:bg-teal-500 rounded-lg p-1 md:hidden"><a href="#" class="text-white"><i
                            class="fas fa-layer-group"></i></a></li>
                <li @click="openChatModal" class="hover:bg-teal-500 rounded-lg p-1 md:hidden cursor-pointer"><a href="#"
                        class="text-white"><i class="fas fa-comments"></i></a></li>
            </ul>
        </div>
    </nav>
    <ChatModal ref="chatModal" />
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const chatModal = ref<{ openModal: () => void } | null>(null)

const openChatModal = () => {
    chatModal.value?.openModal()
}
</script>

<style scoped>
/* Scoped styles for your component if needed */
</style>