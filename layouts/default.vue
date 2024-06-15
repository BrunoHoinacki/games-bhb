<template>
    <div>
        <AppHeader />
        <main class="pt-20 pb-20"> 
            <slot />
        </main>
        <AppFooter />
    </div>
</template>

<script setup lang="ts">
</script>

<style>
/* Global styles */
body {
    @apply bg-teal-800;
}
</style>