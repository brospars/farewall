<script setup lang="ts">
useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'icon', href: '/favicon.ico' },
    { rel: 'preconnect', href: 'https://fonts.googleapis.com' },
    { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: '' },
    { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600;9..144,700&family=Manrope:wght@400;500;600;700;800&display=swap' }
  ],
  htmlAttrs: { lang: 'en' }
})

useSeoMeta({
  title: 'Farewall — Beautiful digital farewell walls',
  description: 'Create a beautiful digital farewell wall in 30 seconds. Your team adds messages, photos, and videos — gift them a memory that lasts forever.',
  ogTitle: 'Farewall — Beautiful digital farewell walls',
  ogDescription: 'Create a beautiful digital farewell wall in 30 seconds.',
  twitterCard: 'summary_large_image'
})

function scrollToCreate() {
  document.getElementById('create')?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <UApp>
    <UHeader :ui="{ root: 'bg-[#fff9f3]/85 backdrop-blur-md border-b border-orange-100/50' }">
      <template #left>
        <NuxtLink to="/" class="flex items-center">
          <AppLogo />
        </NuxtLink>
        <nav class="hidden md:flex items-center gap-6 ml-8">
          <NuxtLink to="/#how-it-works" class="text-sm font-semibold text-muted hover:text-highlighted transition-colors">
            How it works
          </NuxtLink>
          <NuxtLink to="/#pricing" class="text-sm font-semibold text-muted hover:text-highlighted transition-colors">
            Pricing
          </NuxtLink>
          <NuxtLink to="/#faq" class="text-sm font-semibold text-muted hover:text-highlighted transition-colors">
            FAQ
          </NuxtLink>
        </nav>
      </template>

      <template #right>
        <UButton
          size="sm"
          label="Create a Wall"
          color="primary"
          class="!rounded-full warm-shadow font-semibold"
          @click="scrollToCreate"
        />
      </template>
    </UHeader>

    <UMain>
      <NuxtPage />
    </UMain>

    <footer class="border-t border-orange-100/60 bg-[#fff9f3] py-8">
      <div class="max-w-7xl mx-auto px-5 sm:px-8 flex flex-col sm:flex-row items-center justify-between gap-4">
        <NuxtLink to="/">
          <AppLogo />
        </NuxtLink>
        <p class="text-xs text-muted">© {{ new Date().getFullYear() }} Farewall · Made with love</p>
        <div class="flex items-center gap-5">
          <NuxtLink to="/privacy" class="text-xs text-muted hover:text-highlighted transition-colors">Privacy</NuxtLink>
          <NuxtLink to="/terms" class="text-xs text-muted hover:text-highlighted transition-colors">Terms</NuxtLink>
        </div>
      </div>
    </footer>
  </UApp>
</template>
