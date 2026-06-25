<script setup lang="ts">
useSeoMeta({
  title: 'Create a Farewall',
  description: 'Create a beautiful digital farewell wall in 30 seconds. No account needed.'
})

const route = useRoute()
const isPremium = route.query.plan === 'premium'

const occasions = [
  { label: 'Departure / Leaving', value: 'departure' },
  { label: 'Retirement', value: 'retirement' },
  { label: 'Wedding', value: 'wedding' },
  { label: 'Birthday', value: 'birthday' },
  { label: 'New Baby', value: 'birth' },
  { label: 'Moving Away', value: 'moving' },
  { label: 'In Memory Of', value: 'death' },
  { label: 'Other', value: 'other' }
]

const form = reactive({
  recipientName: '',
  occasion: '',
  organizerName: '',
  email: ''
})

const formErrors = reactive({
  recipientName: '',
  occasion: '',
  organizerName: ''
})

const wallCreated = ref(false)
const shareLink = ref('')
const creating = ref(false)

async function createWall() {
  formErrors.recipientName = ''
  formErrors.occasion = ''
  formErrors.organizerName = ''

  if (!form.recipientName.trim()) formErrors.recipientName = 'Please enter the recipient\'s name'
  if (!form.occasion) formErrors.occasion = 'Please select an occasion'
  if (!form.organizerName.trim()) formErrors.organizerName = 'Please enter your name'

  if (formErrors.recipientName || formErrors.occasion || formErrors.organizerName) return

  creating.value = true
  await new Promise(resolve => setTimeout(resolve, 900))
  creating.value = false
  wallCreated.value = true
  shareLink.value = `farewall.com/wall/${Math.random().toString(36).slice(2, 10)}`
}

function copyShareLink() {
  navigator.clipboard.writeText(`https://${shareLink.value}`)
}
</script>

<template>
  <div class="relative min-h-[80vh] overflow-hidden bg-[#fff9f3] px-5 py-16 sm:px-8">
    <div class="orb left-[-4rem] top-0 size-64 bg-[#ffd4b9]" />
    <div class="orb right-[-4rem] bottom-0 size-72 bg-[#f1c090]" />

    <div class="relative mx-auto max-w-lg">
      <div v-if="!wallCreated">
        <div class="text-center mb-10">
          <div class="mx-auto mb-5 size-14 rounded-[1rem] bg-orange-100 flex items-center justify-center">
            <UIcon name="i-lucide-wand-sparkles" class="size-7 text-orange-600" />
          </div>
          <h1 class="text-3xl tracking-[-0.03em] text-orange-950">
            Create a {{ isPremium ? 'Premium' : 'free' }} farewell wall
          </h1>
          <p class="mt-2 text-orange-800/60">Takes 30 seconds · No account needed</p>
          <div v-if="isPremium" class="mt-4 inline-flex items-center gap-2 rounded-full border border-orange-200/70 bg-[#fff4df] px-4 py-2 text-xs font-semibold text-orange-600">
            ⭐ Video, audio, unlimited contributors, forever
          </div>
        </div>

        <div class="glass-panel rounded-[2rem] p-8 warm-shadow-lg space-y-5">
          <UFormField label="Who is this wall for?" :error="formErrors.recipientName" required>
            <UInput v-model="form.recipientName" placeholder="e.g. Sarah Johnson" size="lg" class="w-full" />
          </UFormField>

          <UFormField label="What's the occasion?" :error="formErrors.occasion" required>
            <USelect v-model="form.occasion" :items="occasions" placeholder="Select an occasion" size="lg" class="w-full" />
          </UFormField>

          <UFormField label="Your name" :error="formErrors.organizerName" required>
            <UInput v-model="form.organizerName" placeholder="e.g. Marcus (the organizer)" size="lg" class="w-full" />
          </UFormField>

          <UFormField label="Your email" hint="Optional — for wall notifications">
            <UInput v-model="form.email" type="email" placeholder="you@company.com" size="lg" class="w-full" />
          </UFormField>

          <button
            class="w-full rounded-full bg-orange-600 py-4 text-base font-semibold text-white warm-shadow hover:-translate-y-0.5 hover:bg-orange-700 transition-all flex items-center justify-center gap-2 mt-2"
            :disabled="creating"
            @click="createWall"
          >
            <UIcon v-if="creating" name="i-lucide-loader-circle" class="size-4 animate-spin" />
            <span>{{ creating ? 'Creating your wall…' : isPremium ? 'Create Wall & Upgrade →' : 'Create a Free Wall →' }}</span>
          </button>
          <p class="text-xs text-center text-orange-700/45">
            {{ isPremium ? 'You\'ll be redirected to Stripe after creation.' : 'Free forever · No credit card required' }}
          </p>
        </div>
      </div>

      <!-- Success state -->
      <div v-else class="text-center">
        <div class="font-display text-6xl mb-4">🎉</div>
        <h2 class="text-3xl tracking-[-0.03em] text-orange-950 mb-3">Your wall is ready!</h2>
        <p class="text-orange-800/60 mb-8">Share this link with your team so they can add their messages.</p>
        <div class="glass-panel rounded-[1.5rem] p-4 flex items-center gap-3 mb-6 warm-shadow-lg">
          <code class="flex-1 text-sm text-orange-700 font-semibold truncate text-left">https://{{ shareLink }}</code>
          <button
            class="shrink-0 rounded-full bg-orange-600 px-4 py-2 text-xs font-semibold text-white hover:bg-orange-700 transition-colors"
            @click="copyShareLink"
          >
            Copy link
          </button>
        </div>
        <NuxtLink to="/" class="text-sm text-orange-700/60 hover:text-orange-700 transition-colors">← Back to home</NuxtLink>
      </div>
    </div>
  </div>
</template>
