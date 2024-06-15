<template>
  <div>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(1rem);
}
</style>

<script setup lang="ts">
useSeoMeta({
  title: 'Joga-Aqui.com - Os Melhores Jogos Online para Crianças',
  ogTitle: 'Joga-Aqui.com - Jogos Divertidos e Educativos para Crianças',
  description: 'Descubra os melhores jogos online gratuitos para crianças no Joga-Aqui.com! Diversão garantida com jogos educativos, quebra-cabeças, aventuras e muito mais.',
  ogDescription: 'No Joga-Aqui.com, você encontra uma variedade de jogos online gratuitos e seguros para crianças. Venha se divertir com jogos educativos, quebra-cabeças, aventuras e muito mais.',
  ogImage: '/images/logo-fundo-azul.png',
  twitterCard: 'summary_large_image',
  twitterTitle: 'Joga-Aqui.com - Jogos Online para Crianças',
  twitterDescription: 'Jogue os melhores jogos online gratuitos para crianças no Joga-Aqui.com. Diversão e aprendizado garantidos!',
  twitterImage: '/images/logo-fundo-azul.png',
  keywords: 'jogos online, jogos para crianças, jogos educativos, jogos gratuitos, diversão infantil, jogos seguros',
  robots: 'index, follow',
})
</script>
