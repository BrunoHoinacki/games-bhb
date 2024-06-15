<template>
    <nav class="bg-teal-500 fixed w-full top-0 z-50 shadow-md bg-opacity-60 backdrop-blur border-b border-gray-400">
        <div class="container mx-auto flex justify-between items-center pt-2 px-4 pb-2">
            <a href="/" class="text-white text-xl font-bold">
                <img class="h-14" src="/public/images/logo-sem-fundo.png" alt="Logo">
            </a>
            <ul class="flex space-x-4">
                <li><a href="#" class="text-white hover:underline hidden md:inline">Home</a></li>
                <li><a href="#" class="text-white hover:underline hidden md:inline">Games</a></li>
                <li><a href="#" class="text-white hover:underline hidden md:inline">Contact</a></li>
                <li><a href="#" class="text-white hover:underline md:hidden"><i class="fas fa-home"></i></a></li>
                <li><a href="#" class="text-white hover:underline md:hidden"><i class="fas fa-layer-group"></i></a></li>
                <li><a href="#" class="text-white hover:underline md:hidden"><i class="fas fa-headset"></i></a></li>
            </ul>
        </div>
    </nav>
</template>

<script setup lang="ts">
// Your script setup
</script>

<style scoped>
/* Scoped styles for your component if needed */
</style>