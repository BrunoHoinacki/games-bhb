<template>
    <div class="flex justify-center items-center space-x-2">
        <div class="bg-yellow-500 p-2 w-4 h-4 rounded-full bounce-ball"></div>
        <div class="bg-yellow-500 p-2 w-4 h-4 rounded-full bounce-ball animation-delay-200"></div>
        <div class="bg-yellow-500 p-2 w-4 h-4 rounded-full bounce-ball animation-delay-400"></div>
    </div>
</template>

<script setup lang="ts">
// No specific script setup is needed for this component
</script>

<style scoped>
.bounce-ball {
    animation: bounce 1s infinite;
}

.animation-delay-200 {
    animation-delay: 0.2s;
}

.animation-delay-400 {
    animation-delay: 0.4s;
}

@keyframes bounce {

    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-1rem);
    }
}
</style>