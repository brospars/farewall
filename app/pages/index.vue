<script setup lang="ts">
useSeoMeta({
  title: 'Farewall — Give your colleague the farewell they\'ll never forget',
  description: 'Create a beautiful digital farewell wall in 30 seconds. Your team adds messages, photos, videos — and you gift them a memory that lasts forever.'
})

const steps = [
  {
    icon: 'i-lucide-wand-sparkles',
    title: 'Create a wall',
    description: 'Enter the recipient\'s name and pick the occasion. Takes 30 seconds, no account needed.'
  },
  {
    icon: 'i-lucide-share-2',
    title: 'Share the link',
    description: 'Send the invite link to your team. They add messages, photos, and videos at their own pace.'
  },
  {
    icon: 'i-lucide-gift',
    title: 'Gift the wall',
    description: 'Reveal the finished wall to the recipient — a beautiful memory they\'ll revisit forever.'
  }
]

const features = [
  { icon: 'i-lucide-message-square-heart', label: 'Text messages from the heart', premium: false },
  { icon: 'i-lucide-image', label: 'Photo memories', premium: false },
  { icon: 'i-lucide-link', label: 'Simple share link', premium: false },
  { icon: 'i-lucide-users', label: 'No sign-up for contributors', premium: false },
  { icon: 'i-lucide-video', label: 'Video messages', premium: true },
  { icon: 'i-lucide-mic', label: 'Audio notes', premium: true },
  { icon: 'i-lucide-palette', label: 'Custom themes', premium: true },
  { icon: 'i-lucide-download', label: 'Download as keepsake', premium: true },
  { icon: 'i-lucide-infinity', label: 'Wall lives forever', premium: true },
  { icon: 'i-lucide-users-round', label: 'Unlimited contributors', premium: true },
  { icon: 'i-lucide-badge-check', label: 'Premium badge', premium: true },
  { icon: 'i-lucide-file-text', label: 'HTML & PDF export', premium: true }
]

const testimonials = [
  {
    quote: 'Sarah made our team lead\'s farewell wall and he literally cried. Best $7 we ever spent.',
    name: 'Jessica M.',
    role: 'Team Lead at Notion',
    initials: 'JM',
    bg: 'bg-orange-100',
    text: 'text-orange-800'
  },
  {
    quote: 'So much better than passing around a card. Everyone could contribute at their own pace, even from different time zones.',
    name: 'Tom K.',
    role: 'Engineering Manager at Shopify',
    initials: 'TK',
    bg: 'bg-[#ffe7d6]',
    text: 'text-orange-700'
  },
  {
    quote: 'The video messages were the highlight. You could genuinely feel the love. Our colleague was absolutely speechless.',
    name: 'Priya S.',
    role: 'People Partner at Figma',
    initials: 'PS',
    bg: 'bg-orange-200',
    text: 'text-orange-900'
  }
]

const faqItems = [
  {
    label: 'Is it really free?',
    content: 'Yes! Basic walls are 100% free — no credit card required. You get text and photo messages, up to 20 contributors, and a 90-day wall. Upgrade to Premium for $6.99 to unlock video, audio, unlimited contributors, and a permanent wall.'
  },
  {
    label: 'Does the recipient need to sign up?',
    content: 'No. The recipient just opens a link — no account needed. They can view all the messages and revisit their wall anytime.'
  },
  {
    label: 'How long does the wall last?',
    content: 'Free walls last 90 days from creation. Premium walls last forever. You\'ll receive email reminders before your wall expires with an option to upgrade.'
  },
  {
    label: 'Can contributors add messages after the farewell?',
    content: 'Yes! Contributors can add messages at any time before the wall expires. Great for teams spread across time zones.'
  },
  {
    label: 'Is the wall private?',
    content: 'Yes. Only people with the invite link can see or contribute to the wall. The wall is never publicly listed or discoverable.'
  }
]

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

function scrollToCreate() {
  document.getElementById('create')?.scrollIntoView({ behavior: 'smooth' })
}

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

function resetForm() {
  wallCreated.value = false
  shareLink.value = ''
  Object.assign(form, { recipientName: '', occasion: '', organizerName: '', email: '' })
  Object.assign(formErrors, { recipientName: '', occasion: '', organizerName: '' })
}
</script>

<template>
  <div class="bg-[#fff9f3]">

    <!-- ─── 1. HERO ─────────────────────────────────────────────────── -->
    <section class="relative overflow-hidden px-5 pb-16 pt-10 sm:px-8 sm:pb-24 sm:pt-14 lg:px-10">
      <!-- Atmospheric orbs -->
      <div class="orb left-[-5rem] top-16 size-52 bg-[#ffd4b9]" />
      <div class="orb right-[-4rem] top-24 size-72 bg-[#f1c090]" />
      <div class="orb bottom-0 left-1/3 size-64 bg-[#ffe7d6]" />

      <div class="relative mx-auto max-w-7xl">
        <div class="grid items-center gap-10 lg:grid-cols-[1.05fr_0.95fr] lg:gap-16">

          <!-- Copy -->
          <div class="fade-up max-w-2xl">
            <div class="mb-5 inline-flex items-center rounded-full border border-white/55 bg-white/72 px-4 py-2 text-sm font-medium text-orange-700 shadow-[0_12px_32px_rgba(106,56,35,0.08)]">
              ✨ The thoughtful way to say goodbye
            </div>
            <h1 class="balance text-5xl font-semibold leading-[0.92] tracking-[-0.04em] text-orange-950 sm:text-6xl lg:text-7xl">
              Give your colleague the farewell they'll never forget
            </h1>
            <p class="mt-6 max-w-xl text-lg leading-8 text-orange-800/70 sm:text-xl">
              Create a beautiful digital farewell wall in 30 seconds. Your team adds messages, photos, videos — and you gift them a memory that lasts forever.
            </p>
            <div class="mt-8 flex flex-col gap-4 sm:flex-row">
              <button
                class="warm-shadow rounded-full bg-orange-600 px-7 py-4 text-center text-base font-semibold text-white hover:-translate-y-0.5 hover:bg-orange-700 transition-all"
                @click="scrollToCreate"
              >
                Create a Free Wall →
              </button>
              <NuxtLink
                to="/wall/demo"
                class="rounded-full border border-orange-200/80 bg-white/75 px-7 py-4 text-center text-base font-semibold text-orange-900 hover:-translate-y-0.5 hover:bg-white transition-all"
              >
                See an example wall →
              </NuxtLink>
            </div>
            <p class="mt-5 text-sm text-orange-700/50">Free forever · No credit card · 30 seconds to create</p>
          </div>

          <!-- Wall mockup -->
          <div class="relative">
            <div class="absolute inset-x-10 top-6 h-24 rounded-full bg-[radial-gradient(circle,rgba(255,215,165,0.7),transparent_72%)] blur-2xl" />
            <div class="soft-outline relative overflow-hidden rounded-[2.2rem] border border-white/60 bg-[linear-gradient(180deg,rgba(255,249,243,0.97),rgba(255,236,219,0.86))] p-5 warm-shadow-lg sm:p-7">
              <!-- Wall header card -->
              <div class="relative rounded-[1.7rem] border border-white/65 bg-[#fff8f2]/95 p-5 shadow-[inset_0_1px_0_rgba(255,255,255,0.8)] sm:p-6">
                <div class="flex items-start justify-between gap-4">
                  <div>
                    <div class="text-xs font-semibold uppercase tracking-[0.22em] text-orange-600/70">Farewall for</div>
                    <h3 class="mt-2 text-3xl text-orange-950 sm:text-4xl">Sarah Johnson 🎉</h3>
                  </div>
                  <div class="rounded-[1.2rem] border border-white/70 bg-white px-4 py-3 text-right shadow-[0_12px_24px_rgba(106,56,35,0.08)]">
                    <div class="text-xs font-semibold uppercase tracking-[0.16em] text-orange-500/70">Messages</div>
                    <div class="font-display mt-1 text-3xl text-orange-950">38</div>
                  </div>
                </div>

                <!-- Sample message cards -->
                <div class="mt-5 grid gap-3">
                  <div class="rotate-[-1.5deg] rounded-[1.4rem] bg-white p-4 shadow-[0_16px_36px_rgba(106,56,35,0.09)]">
                    <div class="flex items-center gap-2 mb-2">
                      <div class="size-6 rounded-full bg-orange-100 text-orange-700 text-xs flex items-center justify-center font-bold shrink-0">M</div>
                      <span class="text-xs font-semibold text-orange-600">Marcus T.</span>
                    </div>
                    <p class="text-sm leading-6 text-orange-900/70">"You've been the heart of our team. We'll miss you so much! 💙"</p>
                  </div>
                  <div class="grid grid-cols-[1.1fr_0.9fr] gap-3">
                    <div class="translate-x-2 rounded-[1.4rem] bg-[#ffe7d6] p-4 shadow-[0_16px_36px_rgba(106,56,35,0.09)]">
                      <div class="text-xs font-semibold text-orange-600 mb-2">Lisa K. · Photo</div>
                      <div class="grid grid-cols-3 gap-1.5">
                        <div class="h-10 rounded-xl bg-[#f2bf97]" />
                        <div class="h-10 rounded-xl bg-[#f6d6b8]" />
                        <div class="h-10 rounded-xl bg-[#ebb184]" />
                      </div>
                    </div>
                    <div class="translate-y-3 rounded-[1.4rem] bg-[#fff4df] p-4 shadow-[0_16px_36px_rgba(106,56,35,0.09)]">
                      <div class="text-xs font-semibold text-orange-600 mb-2">James R.</div>
                      <p class="text-xs leading-5 text-orange-900/70 space-y-1">"Best colleague ever! 🚀"</p>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Contributor avatars -->
              <div class="mt-4 flex items-center justify-between px-1">
                <span class="text-xs font-medium text-orange-700/60">34 more messages...</span>
                <div class="flex -space-x-2">
                  <div v-for="(a, i) in [['T', '#f6b895'], ['P', '#e8916a'], ['K', '#c9683a'], ['+', '#9f452d']]" :key="i"
                    class="size-7 rounded-full border-2 border-[#fff9f3] flex items-center justify-center text-white text-xs font-bold"
                    :style="{ backgroundColor: a[1] }"
                  >
                    {{ a[0] }}
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ─── 2. SOCIAL PROOF ──────────────────────────────────────────── -->
    <section class="border-y border-orange-100/60 bg-[#fff4ec]/50 py-10">
      <div class="mx-auto max-w-7xl px-5 sm:px-8">
        <p class="text-center text-xs font-semibold uppercase tracking-[0.22em] text-orange-600/60 mb-6">Trusted by teams at</p>
        <div class="flex flex-wrap items-center justify-center gap-8 mb-8">
          <UIcon
            v-for="logo in ['i-simple-icons-figma', 'i-simple-icons-notion', 'i-simple-icons-shopify', 'i-simple-icons-stripe', 'i-simple-icons-vercel', 'i-simple-icons-linear']"
            :key="logo"
            :name="logo"
            class="size-6 text-orange-300 hover:text-orange-400 transition-colors"
          />
        </div>
        <div class="flex flex-wrap items-center justify-center gap-12 text-center">
          <div v-for="[val, label] in [['1,000+', 'walls created'], ['15,000+', 'heartfelt messages'], ['4.9 / 5', 'organizer rating']]" :key="label">
            <div class="font-display text-3xl font-semibold text-orange-700">{{ val }}</div>
            <div class="mt-1 text-sm text-orange-700/60">{{ label }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- ─── 3. HOW IT WORKS ──────────────────────────────────────────── -->
    <section id="how-it-works" class="relative overflow-hidden py-24 lg:py-32">
      <div class="orb right-[-6rem] top-20 size-80 bg-[#ffd4b9]" />
      <div class="mx-auto max-w-7xl px-5 sm:px-8 lg:px-10">
        <div class="max-w-2xl">
          <p class="text-xs font-semibold uppercase tracking-[0.22em] text-orange-600/70">Simple process</p>
          <h2 class="mt-3 text-4xl tracking-[-0.04em] text-orange-950 sm:text-5xl">How it works</h2>
          <p class="mt-4 text-lg text-orange-800/60">Three simple steps to create a farewell they'll cherish forever.</p>
        </div>
        <div class="mt-12 grid gap-5 lg:grid-cols-3">
          <div v-for="(step, i) in steps" :key="i" class="glass-panel rounded-[1.9rem] p-6 warm-shadow-lg sm:p-7">
            <div class="flex items-center justify-between">
              <div class="size-12 rounded-[0.9rem] bg-orange-100 flex items-center justify-center">
                <UIcon :name="step.icon" class="size-6 text-orange-600" />
              </div>
              <span class="font-display text-5xl leading-none text-orange-200 font-semibold">0{{ i + 1 }}</span>
            </div>
            <h3 class="mt-5 text-2xl tracking-tight text-orange-950">{{ step.title }}</h3>
            <p class="mt-3 text-base leading-7 text-orange-800/65">{{ step.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ─── 4. FEATURE SHOWCASE ──────────────────────────────────────── -->
    <section class="relative overflow-hidden py-24 bg-[#fff4ec]/40">
      <div class="orb left-[-4rem] bottom-0 size-72 bg-[#f1c090]" />
      <div class="mx-auto max-w-7xl px-5 sm:px-8 lg:px-10">
        <div class="text-center max-w-2xl mx-auto mb-12">
          <p class="text-xs font-semibold uppercase tracking-[0.22em] text-orange-600/70">What's included</p>
          <h2 class="mt-3 text-4xl tracking-[-0.04em] text-orange-950 sm:text-5xl">Everything you need for the perfect farewell</h2>
        </div>
        <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
          <div
            v-for="feature in features"
            :key="feature.label"
            class="rounded-[1.4rem] border border-white/70 bg-white/70 p-5 backdrop-blur-sm hover:bg-white/90 hover:shadow-[0_12px_32px_rgba(106,56,35,0.08)] transition-all"
          >
            <div class="flex items-start gap-3">
              <div class="size-9 rounded-xl flex items-center justify-center shrink-0"
                :class="feature.premium ? 'bg-[#fff4df] text-orange-400' : 'bg-orange-100 text-orange-600'">
                <UIcon :name="feature.icon" class="size-4" />
              </div>
              <div class="pt-0.5">
                <p class="text-sm font-medium text-orange-950 leading-snug">{{ feature.label }}</p>
                <span v-if="feature.premium" class="mt-1.5 inline-flex rounded-full border border-orange-200/70 bg-[#fff4df] px-2 py-0.5 text-xs font-semibold text-orange-500">
                  Premium
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ─── 5. PRICING ───────────────────────────────────────────────── -->
    <section id="pricing" class="relative overflow-hidden py-24 lg:py-32">
      <div class="orb right-0 top-1/2 size-80 bg-[#ffe7d6]" />
      <div class="mx-auto max-w-7xl px-5 sm:px-8 lg:px-10">
        <div class="max-w-2xl mb-12">
          <p class="text-xs font-semibold uppercase tracking-[0.22em] text-orange-600/70">Pricing</p>
          <h2 class="mt-3 text-4xl tracking-[-0.04em] text-orange-950 sm:text-5xl">Simple, honest pricing</h2>
          <p class="mt-4 text-lg text-orange-800/60">Pay once per wall. No subscriptions, no surprises.</p>
        </div>

        <div class="grid md:grid-cols-2 gap-6 max-w-3xl">
          <!-- Free tier -->
          <div class="rounded-[2rem] border border-orange-100/80 bg-[linear-gradient(180deg,rgba(255,243,229,0.96),rgba(255,251,246,0.86))] p-7 warm-shadow-lg flex flex-col">
            <div class="mb-6">
              <p class="text-xs font-semibold uppercase tracking-[0.22em] text-orange-600/70">Free</p>
              <div class="font-display mt-2 text-5xl text-orange-950">$0</div>
              <p class="mt-1 text-sm text-orange-700/60">No credit card needed</p>
            </div>
            <ul class="space-y-3 flex-1 mb-7">
              <li
                v-for="item in ['Text & photo messages', 'Up to 20 contributors', '90-day wall life', 'Default theme', 'Simple share link']"
                :key="item"
                class="flex items-center gap-3 text-sm text-orange-900/75"
              >
                <UIcon name="i-lucide-check" class="size-4 text-orange-500 shrink-0" />
                {{ item }}
              </li>
            </ul>
            <button
              class="w-full rounded-full border border-orange-300/60 bg-white/80 py-3.5 text-sm font-semibold text-orange-800 hover:-translate-y-0.5 hover:bg-white transition-all"
              @click="scrollToCreate"
            >
              Create a Free Wall
            </button>
          </div>

          <!-- Premium tier -->
          <div class="relative overflow-hidden rounded-[2rem] bg-gradient-to-b from-orange-600 to-orange-800 p-7 warm-shadow flex flex-col text-white">
            <div class="absolute inset-x-8 top-0 h-px bg-gradient-to-r from-transparent via-white/40 to-transparent" />
            <div class="absolute top-5 right-5 rounded-full border border-white/25 bg-white/15 px-3 py-1 text-xs font-semibold uppercase tracking-[0.16em]">
              Most loved
            </div>
            <div class="mb-6">
              <p class="text-xs font-semibold uppercase tracking-[0.22em] opacity-70">Premium</p>
              <div class="font-display mt-2 flex items-baseline gap-1">
                <span class="text-5xl">$6.99</span>
                <span class="opacity-60 text-sm">/wall</span>
              </div>
              <p class="mt-1 text-sm opacity-60">One-time · No subscription</p>
            </div>
            <ul class="space-y-3 flex-1 mb-7">
              <li
                v-for="item in ['Everything in Free', 'Video & audio messages', 'Unlimited contributors', 'Wall never expires', '5 custom themes', 'HTML & PDF export', 'Premium badge']"
                :key="item"
                class="flex items-center gap-3 text-sm"
                :class="item === 'Everything in Free' ? 'opacity-60' : ''"
              >
                <UIcon name="i-lucide-check" class="size-4 shrink-0" />
                {{ item }}
              </li>
            </ul>
            <NuxtLink
              to="/create?plan=premium"
              class="block w-full rounded-full bg-white py-3.5 text-center text-sm font-semibold text-orange-700 hover:-translate-y-0.5 hover:bg-orange-50 transition-all"
            >
              Create a Wall &amp; Upgrade
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

    <!-- ─── 6. TESTIMONIALS ──────────────────────────────────────────── -->
    <section class="relative overflow-hidden py-24 bg-[#fff4ec]/40">
      <div class="orb left-1/2 top-0 size-96 bg-[#ffd4b9]" />
      <div class="mx-auto max-w-7xl px-5 sm:px-8 lg:px-10">
        <div class="max-w-2xl mb-12">
          <p class="text-xs font-semibold uppercase tracking-[0.22em] text-orange-600/70">Stories</p>
          <h2 class="mt-3 text-4xl tracking-[-0.04em] text-orange-950 sm:text-5xl">People love Farewall</h2>
          <p class="mt-4 text-lg text-orange-800/60">From team leads to HR managers — anyone who's given a Farewall remembers it.</p>
        </div>
        <div class="grid gap-5 md:grid-cols-3">
          <div
            v-for="t in testimonials"
            :key="t.name"
            class="glass-panel rounded-[1.9rem] p-6 warm-shadow-lg sm:p-7 flex flex-col"
          >
            <div class="flex gap-0.5 mb-5">
              <UIcon v-for="n in 5" :key="n" name="i-lucide-star" class="size-4 text-orange-400" />
            </div>
            <p class="text-base leading-7 text-orange-900/75 flex-1 mb-6">"{{ t.quote }}"</p>
            <div class="flex items-center gap-3">
              <div class="size-10 rounded-full flex items-center justify-center text-sm font-bold shrink-0" :class="[t.bg, t.text]">
                {{ t.initials }}
              </div>
              <div>
                <p class="font-semibold text-orange-950 text-sm">{{ t.name }}</p>
                <p class="text-orange-700/55 text-xs mt-0.5">{{ t.role }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ─── 7. FAQ ────────────────────────────────────────────────────── -->
    <section id="faq" class="py-24 lg:py-32">
      <div class="mx-auto max-w-2xl px-5 sm:px-8">
        <div class="mb-12">
          <p class="text-xs font-semibold uppercase tracking-[0.22em] text-orange-600/70">Questions</p>
          <h2 class="mt-3 text-4xl tracking-[-0.04em] text-orange-950 sm:text-5xl">Frequently asked questions</h2>
        </div>
        <UAccordion
          :items="faqItems"
          :ui="{
            item: 'border-b border-orange-100',
            label: 'text-orange-950 font-semibold text-base',
            content: 'text-orange-800/70 leading-7'
          }"
        />
      </div>
    </section>

    <!-- ─── 8. FINAL CTA + CREATE FORM ──────────────────────────────── -->
    <section id="create" class="relative overflow-hidden py-24 lg:py-32 bg-[#fff4ec]/40">
      <div class="orb left-[-4rem] top-0 size-72 bg-[#ffd4b9]" />
      <div class="orb right-[-4rem] bottom-0 size-64 bg-[#f1c090]" />

      <div class="relative mx-auto max-w-xl px-5 sm:px-8">
        <!-- Form state -->
        <div v-if="!wallCreated">
          <div class="mb-10 text-center">
            <h2 class="text-4xl tracking-[-0.04em] text-orange-950 sm:text-5xl">
              Someone's last day is coming.
              <span class="text-orange-600"> Make it unforgettable.</span>
            </h2>
            <p class="mt-4 text-orange-800/60">Free to start · No account needed · Ready in 30 seconds</p>
          </div>

          <div class="glass-panel rounded-[2rem] p-8 warm-shadow-lg space-y-5">
            <UFormField label="Who is this wall for?" :error="formErrors.recipientName" required>
              <UInput
                v-model="form.recipientName"
                placeholder="e.g. Sarah Johnson"
                size="lg"
                class="w-full"
              />
            </UFormField>

            <UFormField label="What's the occasion?" :error="formErrors.occasion" required>
              <USelect
                v-model="form.occasion"
                :items="occasions"
                placeholder="Select an occasion"
                size="lg"
                class="w-full"
              />
            </UFormField>

            <UFormField label="Your name" :error="formErrors.organizerName" required>
              <UInput
                v-model="form.organizerName"
                placeholder="e.g. Marcus (the organizer)"
                size="lg"
                class="w-full"
              />
            </UFormField>

            <UFormField label="Your email" hint="Optional — for wall notifications">
              <UInput
                v-model="form.email"
                type="email"
                placeholder="you@company.com"
                size="lg"
                class="w-full"
              />
            </UFormField>

            <button
              class="w-full rounded-full bg-orange-600 py-4 text-base font-semibold text-white warm-shadow hover:-translate-y-0.5 hover:bg-orange-700 transition-all flex items-center justify-center gap-2 mt-2"
              :disabled="creating"
              @click="createWall"
            >
              <UIcon v-if="creating" name="i-lucide-loader-circle" class="size-4 animate-spin" />
              <span>{{ creating ? 'Creating your wall…' : 'Create a Free Wall →' }}</span>
            </button>
            <p class="text-xs text-center text-orange-700/45">Free forever · No credit card required</p>
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
          <button class="text-sm text-orange-700/60 hover:text-orange-700 transition-colors" @click="resetForm">
            ← Create another wall
          </button>
        </div>
      </div>
    </section>

  </div>
</template>
