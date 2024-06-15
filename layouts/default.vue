<template>
    <div>
        <AppHeader />
        <main class="pt-16"> <!-- Adjust the padding-top based on the height of your navbar -->
            <slot />
        </main>
        <AppFooter />
    </div>
</template>

<script setup lang="ts">
import AppHeader from '@/components/AppHeader.vue'
import AppFooter from '@/components/AppFooter.vue'
</script>

<style>
/* Global styles */
body {
    @apply bg-teal-800;
}
</style>