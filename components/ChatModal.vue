<template>
    <div v-if="isVisible" class="fixed inset-0 bg-gray-800 bg-opacity-75 flex justify-center items-center z-50"
        @click="closeModal">
        <div class="bg-white rounded-lg overflow-hidden shadow-xl transform transition-all sm:max-w-lg sm:w-full"
            @click.stop>
            <div class="bg-teal-500 p-4">
                <h2 class="text-white text-xl font-bold">Chat</h2>
            </div>
            <div class="p-4">
                <!-- Chat content goes here -->
                <p class="text-gray-700">Welcome to the chat modal!</p>
            </div>
            <div class="bg-gray-100 p-4 flex justify-end">
                <button @click="closeModal" class="bg-teal-500 text-white px-4 py-2 rounded-lg">
                    Close
                </button>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'

const isVisible = ref(false)

const openModal = () => {
    isVisible.value = true
    document.body.classList.add('modal-open')
}

const closeModal = () => {
    isVisible.value = false
    document.body.classList.remove('modal-open')
}

defineExpose({ openModal, closeModal })

watch(isVisible, (newValue) => {
    if (newValue) {
        document.body.classList.add('modal-open')
    } else {
        document.body.classList.remove('modal-open')
    }
})
</script>

<style scoped>
/* Scoped styles for your component if needed */
</style>

<style global>
.modal-open {
    overflow: hidden;
}
</style>