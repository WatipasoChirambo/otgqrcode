<script setup lang="ts">
import { ref } from 'vue'

const { isNotificationsSlideoverOpen } = useDashboard()

const products = [
  {
    kva: 1,
    price: 4900000,
    desc: 'Ideal for homes, Powers lights, wifi, phone charging.',
    specs: ['Lithium battery', 'Solar panels', 'MUST inverter', 'Installation kit'],
    color: '#BA7517',
    img: '/product.jpg',
  },
  {
    kva: 3,
    price: 8400000,
    desc: 'Ideal for homes. Powers lights, fans, phone charging, a TV and a small fridge.',
    specs: ['Lithium battery', 'Solar panels', 'MUST inverter', 'Installation kit'],
    color: '#1D9E75',
    img: '/product.jpg',
  },
  {
    kva: 5,
    price: 10450000,
    desc: 'Perfect for a medium home. Handles lighting, entertainment, fridge and a small water pump.',
    specs: ['Lithium battery', 'Solar panels', 'MUST inverter', 'MPPT controller'],
    color: '#378ADD',
    img: '/product.png',
  },
  {
    kva: 6,
    price: 11400000,
    tag: 'Most popular',
    desc: 'Our best-seller. Comfortably runs a full household — fridge, TV, lights, fans and more.',
    specs: ['LiFePO4 battery', 'High-yield panels', 'MUST inverter', 'MPPT controller'],
    color: '#534AB7',
    img: '/product.png',
  },
  {
    kva: 12,
    price: 22400000,
    desc: 'Large family home or small office. Supports air conditioning, computers and heavy appliances.',
    specs: ['LiFePO4 battery', 'Dual panel array', 'MUST inverter', 'Smart controller'],
    color: '#D85A30',
    img: '/product.png',
  },
  {
    kva: 20,
    price: 35500000,
    desc: 'Small to medium business. Handles multiple workstations, printers, fridges and security systems.',
    specs: ['Commercial battery', 'Large panel array', '3-phase inverter', 'Monitoring system'],
    color: '#BA7517',
    img: '/product.png',
  },
  {
    kva: 60,
    price: 68500000,
    desc: 'Medium enterprise. Powers full offices, workshops or lodges with heavy equipment.',
    specs: ['Industrial batteries', 'Commercial panels', 'Industrial inverter', 'Remote monitoring'],
    color: '#185FA5',
    img: '/product.png',
  },
  {
    kva: 100,
    price: 92500000,
    desc: 'Large commercial or industrial. Complete off-grid independence for factories and large facilities.',
    specs: ['Industrial battery bank', 'Large-scale panels', 'Industrial inverter', 'Full BMS system'],
    color: '#993C1D',
    img: '/product.png',
  },
]

const swiftLoans = [
  {
    label: 'Personal Loan',
    desc: 'For individuals — quick personal financing',
    url: 'https://swiftcapital.mw/personal-loan-application/',
  },
  {
    label: 'Business Loan',
    desc: 'For businesses — grow with flexible funding',
    url: 'https://swiftcapital.mw/business-loan-application/',
  },
]

const fmt = (n: number) => 'MWK ' + n.toLocaleString()

// Modal state
const modalOpen = ref(false)
const currentPkg = ref<(typeof products)[0] | null>(null)
const currentPlan = ref<'call' | 'swift'>('call')
const checkoutStep = ref<'select' | 'success'>('select')

function openModal(pkg: (typeof products)[0]) {
  currentPkg.value = pkg
  currentPlan.value = 'call'
  checkoutStep.value = 'select'
  modalOpen.value = true
}

function closeModal() {
  modalOpen.value = false
}
</script>

<template>
  <UDashboardPanel id="home">
    <template #body>
      <div class="p-6 space-y-6">

        <!-- Hero section -->
        <div>
          <h1 class="text-4xl md:text-6xl font-semibold tracking-tight leading-tight">
            Clean Energy for
            <span class="bg-gradient-to-r from-violet-600 to-indigo-500 bg-clip-text text-transparent">
              Modern Living
            </span>
          </h1>
          <p class="mt-4 text-gray-500 max-w-xl">
            Reliable solar systems for homes and businesses in Malawi. Built for performance, designed for simplicity.
          </p>
        </div>

        <!-- Promo banner -->
        <div
          class="relative overflow-hidden rounded-2xl border border-violet-100 dark:border-violet-900 bg-gradient-to-br from-violet-50 via-white to-violet-100 dark:from-violet-950 dark:via-gray-900 dark:to-violet-900 p-6 md:p-10">
          <div class="absolute -top-20 -right-20 w-72 h-72 bg-violet-400/20 rounded-full blur-3xl"></div>
          <div class="absolute -bottom-20 -left-20 w-72 h-72 bg-indigo-400/20 rounded-full blur-3xl"></div>

          <div class="relative flex flex-col lg:flex-row items-start lg:items-center justify-between gap-8">
            <div class="max-w-xl">
              <h2 class="text-2xl md:text-3xl font-semibold text-gray-900 dark:text-white leading-tight">
                Power Your Home with
                <span class="text-violet-600">Reliable Solar Energy</span>
              </h2>
              <p class="mt-3 text-sm md:text-base text-gray-600 dark:text-gray-400 leading-relaxed">
                Complete off-grid solar systems designed for Malawi. From small homes to large businesses —
                clean, reliable power with flexible payment options.
              </p>
              <div class="flex flex-wrap gap-2 mt-4">
                <span class="text-xs px-3 py-1 rounded-full bg-violet-100 dark:bg-violet-900 text-violet-700 dark:text-violet-300">⚡ No ESCOM outages</span>
                <span class="text-xs px-3 py-1 rounded-full bg-violet-100 dark:bg-violet-900 text-violet-700 dark:text-violet-300">💳 Swift Capital financing</span>
                <span class="text-xs px-3 py-1 rounded-full bg-violet-100 dark:bg-violet-900 text-violet-700 dark:text-violet-300">🔧 Installation included</span>
                <span class="text-xs px-3 py-1 rounded-full bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300">🎁 FREE Airtel 5G WiFi Router + 2 months unlimited</span>
              </div>
              <div class="flex flex-wrap gap-3 mt-6">
                <a href="#products" class="px-5 py-3 rounded-lg bg-violet-600 text-white text-sm font-medium hover:opacity-90 transition">Browse Systems</a>
                <a href="https://wa.me/265886616931" target="_blank"
                  class="px-5 py-3 rounded-lg border border-gray-200 dark:border-gray-700 text-sm text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-gray-800 transition">
                  Talk to Sales
                </a>
              </div>
            </div>
            <div class="flex-1 flex justify-center lg:justify-end">
              <div class="grid grid-cols-2 gap-3 max-w-xs">
                <div class="rounded-xl p-3 bg-white/70 dark:bg-gray-800/70 border border-gray-200 dark:border-gray-700 backdrop-blur">
                  <div class="text-xs text-gray-400">Starting from</div>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white">3 KVA</div>
                </div>
                <div class="rounded-xl p-3 bg-white/70 dark:bg-gray-800/70 border border-gray-200 dark:border-gray-700 backdrop-blur">
                  <div class="text-xs text-gray-400">Max capacity</div>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white">100 KVA</div>
                </div>
                <div class="rounded-xl p-3 bg-white/70 dark:bg-gray-800/70 border border-gray-200 dark:border-gray-700 backdrop-blur">
                  <div class="text-xs text-gray-400">Coverage</div>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white">Nationwide</div>
                </div>
                <div class="rounded-xl p-3 bg-white/70 dark:bg-gray-800/70 border border-gray-200 dark:border-gray-700 backdrop-blur">
                  <div class="text-xs text-gray-400">Install time</div>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white">2–5 days</div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Product grid -->
        <p class="font-bold text-2xl">Products</p>
        <div id="products" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
          <div v-for="pkg in products" :key="pkg.kva"
            class="rounded-xl border border-gray-200 dark:border-gray-700 bg-white dark:bg-gray-900 flex flex-col overflow-hidden">
            <div class="h-36 flex flex-col items-center justify-center relative" :style="{ background: pkg.color + '18' }">
              <span v-if="pkg.tag" class="absolute top-2 left-2 text-[10px] px-2 py-0.5 rounded-full text-white" :style="{ background: pkg.color }">
                {{ pkg.tag }}
              </span>
              <img src="/product.png" alt="Product" class="w-24 h-24 mb-2 object-contain mt-4" />
              <div class="text-2xl font-semibold" :style="{ color: pkg.color }">{{ pkg.kva }} KVA</div>
            </div>
            <div class="p-3 flex flex-col gap-1.5 flex-1">
              <div class="text-xs text-gray-400">Complete solar system</div>
              <div class="text-xs text-gray-500 dark:text-gray-400 leading-relaxed flex-1">{{ pkg.desc }}</div>
              <div class="flex flex-wrap gap-1 mt-1">
                <span v-for="spec in pkg.specs" :key="spec"
                  class="text-[10px] bg-gray-100 dark:bg-gray-800 text-gray-500 dark:text-gray-400 px-2 py-0.5 rounded">
                  {{ spec }}
                </span>
              </div>
              <div class="text-sm font-medium text-gray-900 dark:text-white mt-1">{{ fmt(pkg.price) }}</div>
              <div class="text-xs text-gray-400">Finance via Swift Capital</div>
              <div class="rounded-lg px-2.5 py-2 text-[10px] font-medium text-white flex items-start gap-1.5" :style="{ background: pkg.color + 'ee' }">
                <span class="text-sm leading-none mt-0.5">🎁</span>
                <span class="leading-snug">FREE <strong>Airtel 5G WiFi Router</strong> + <strong>2 months unlimited access</strong> included!</span>
              </div>
            </div>
            <button
              class="mx-3 mb-3 py-2.5 rounded-lg text-white text-sm font-medium transition-opacity hover:opacity-85"
              :style="{ background: pkg.color }" @click="openModal(pkg)">
              Buy now
            </button>
          </div>
        </div>

        <!-- Footer CTA -->
        <div class="text-center pt-6">
          <div class="text-sm text-gray-500 mb-3">Need help choosing the right system?</div>
          <a href="tel:+265886616931" class="inline-block px-6 py-3 rounded-full bg-violet-600 text-white text-sm font-medium hover:opacity-90">
            Call Now: +265886616931
          </a>
        </div>
      </div>

      <!-- Buy Modal -->
      <Teleport to="body">
        <Transition name="fade">
          <div v-if="modalOpen" class="fixed inset-0 z-50 flex items-center justify-center bg-black/45" @click.self="closeModal">
            <div class="bg-white dark:bg-gray-900 rounded-xl border border-gray-200 dark:border-gray-700 w-full max-w-md mx-4 overflow-hidden max-h-[90vh] overflow-y-auto">

              <!-- Modal header -->
              <div class="flex items-center justify-between px-5 py-4 border-b border-gray-100 dark:border-gray-800 sticky top-0 bg-white dark:bg-gray-900 z-10">
                <span class="text-sm font-medium text-gray-900 dark:text-white">
                  Buy {{ currentPkg?.kva }} KVA system
                </span>
                <button class="text-gray-400 hover:text-gray-600 text-lg leading-none px-1" @click="closeModal">✕</button>
              </div>

              <!-- Step: select plan -->
              <div v-if="checkoutStep === 'select' && currentPkg" class="p-5 space-y-4">

                <!-- Product summary -->
                <div class="bg-gray-50 dark:bg-gray-800 rounded-lg px-4 py-3 flex justify-between items-center">
                  <div class="text-sm font-medium text-gray-900 dark:text-white">{{ currentPkg.kva }} KVA solar system</div>
                  <div class="text-sm text-gray-500">{{ fmt(currentPkg.price) }}</div>
                </div>

                <!-- Payment plan -->
                <div>
                  <div class="text-[11px] text-gray-400 uppercase tracking-wide mb-2">Payment plan</div>
                  <div class="grid grid-cols-2 gap-2">
                    <!-- Call to Order -->
                    <div
                      class="border rounded-lg p-3 text-center cursor-pointer transition-all"
                      :class="currentPlan === 'call' ? 'border-2 border-violet-500 bg-violet-50 dark:bg-violet-950' : 'border-gray-200 dark:border-gray-700'"
                      @click="currentPlan = 'call'">
                      <div class="text-base mb-0.5">📞</div>
                      <div class="text-xs font-medium text-gray-800 dark:text-gray-200">Call to Order</div>
                      <div class="text-[11px] text-gray-400 mt-0.5">Speak with sales</div>
                    </div>
                    <!-- Swift Capital -->
                    <div
                      class="border rounded-lg p-3 text-center cursor-pointer transition-all"
                      :class="currentPlan === 'swift' ? 'border-2 border-violet-500 bg-violet-50 dark:bg-violet-950' : 'border-gray-200 dark:border-gray-700'"
                      @click="currentPlan = 'swift'">
                      <div class="text-base mb-0.5">🏦</div>
                      <div class="text-xs font-medium text-gray-800 dark:text-gray-200">Swift Capital</div>
                      <div class="text-[11px] text-gray-400 mt-0.5">Loan financing</div>
                    </div>
                  </div>
                </div>

                <!-- Swift Capital loan options -->
                <div v-if="currentPlan === 'swift'" class="space-y-2">
                  <div class="text-[11px] text-gray-400 uppercase tracking-wide mb-1">Choose a loan type</div>
                  <a
                    v-for="loan in swiftLoans"
                    :key="loan.url"
                    :href="loan.url"
                    target="_blank"
                    class="flex items-center justify-between rounded-lg border border-gray-200 dark:border-gray-700 px-4 py-3 hover:border-violet-400 hover:bg-violet-50 dark:hover:bg-violet-950 transition-all no-underline group">
                    <div>
                      <div class="text-sm font-medium text-gray-800 dark:text-gray-200 group-hover:text-violet-600">{{ loan.label }}</div>
                      <div class="text-[11px] text-gray-400 mt-0.5">{{ loan.desc }}</div>
                    </div>
                    <span class="text-gray-400 group-hover:text-violet-500 text-lg">→</span>
                  </a>
                  <p class="text-[11px] text-gray-400 pt-1">
                    You'll be taken to Swift Capital's website to complete your loan application. Come back once approved to place your order.
                  </p>
                </div>

                <!-- Call to Order CTA -->
                <div v-if="currentPlan === 'call'" class="space-y-3">
                  <div class="bg-violet-50 dark:bg-violet-950 border border-violet-100 dark:border-violet-900 rounded-lg px-4 py-3 text-center">
                    <p class="text-xs text-gray-500 dark:text-gray-400 leading-relaxed">
                      Call us to place your order for the <strong class="text-gray-800 dark:text-gray-200">{{ currentPkg.kva }} KVA system</strong>. Our sales team will guide you through the process and arrange delivery.
                    </p>
                  </div>
                  <a
                    href="tel:+265886616931"
                    class="flex items-center justify-center gap-2 w-full py-3 rounded-lg bg-violet-600 text-white text-sm font-medium hover:opacity-90 transition-opacity no-underline">
                    📞 Call Now: +265886616931
                  </a>
                  <a
                    href="https://wa.me/265886616931"
                    target="_blank"
                    class="flex items-center justify-center gap-2 w-full py-3 rounded-lg bg-green-500 text-white text-sm font-medium hover:opacity-90 transition-opacity no-underline">
                    💬 WhatsApp Instead
                  </a>
                </div>

              </div>

            </div>
          </div>
        </Transition>
      </Teleport>

    </template>
  </UDashboardPanel>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>