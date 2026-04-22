<script setup lang="ts">
import { ref } from 'vue'

const { isNotificationsSlideoverOpen } = useDashboard()

const products = [
  {
    kva: 3,
    price: 8400000,
    desc: 'Ideal for a small home. Powers lights, fans, phone charging, a TV and a small fridge.',
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
    price: 17400000,
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
const currentPlan = ref<'cash' | 'swift'>('cash')
const currentMethod = ref<'mpamba' | 'airtel' | 'visa'>('visa')
const checkoutStep = ref<'select' | 'pay' | 'success'>('select')

// Pay form fields
const mobileNumber = ref('')
const cardNumber = ref('')
const cardExpiry = ref('')
const cardCvv = ref('')
const cardName = ref('')

function openModal(pkg: (typeof products)[0]) {
  currentPkg.value = pkg
  currentPlan.value = 'cash'
  currentMethod.value = 'visa'
  checkoutStep.value = 'select'
  mobileNumber.value = ''
  cardNumber.value = ''
  cardExpiry.value = ''
  cardCvv.value = ''
  cardName.value = ''
  modalOpen.value = true
}

function closeModal() {
  modalOpen.value = false
}

function dueNow(pkg: (typeof products)[0]) {
  return pkg.price
}

function proceedCheckout() {
  checkoutStep.value = 'pay'
}

function confirmPayment() {
  checkoutStep.value = 'success'
}

function formatCardInput(e: Event) {
  const input = e.target as HTMLInputElement
  const v = input.value.replace(/\D/g, '').substring(0, 16)
  cardNumber.value = v.replace(/(.{4})/g, '$1 ').trim()
}

const methodLabels: Record<string, string> = {
  mpamba: 'Mpamba (TNM)',
  airtel: 'Airtel Money',
  visa: 'Visa card',
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
                  <template v-if="checkoutStep === 'success'">Order confirmed</template>
                  <template v-else>Buy {{ currentPkg?.kva }} KVA system</template>
                </span>
                <button class="text-gray-400 hover:text-gray-600 text-lg leading-none px-1" @click="closeModal">✕</button>
              </div>

              <!-- Step: select plan + method -->
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
                    <!-- Cash -->
                    <div
                      class="border rounded-lg p-3 text-center cursor-pointer transition-all"
                      :class="currentPlan === 'cash' ? 'border-2 border-violet-500 bg-violet-50 dark:bg-violet-950' : 'border-gray-200 dark:border-gray-700'"
                      @click="currentPlan = 'cash'">
                      <div class="text-base mb-0.5">💵</div>
                      <div class="text-xs font-medium text-gray-800 dark:text-gray-200">Cash / Card</div>
                      <div class="text-[11px] text-gray-400 mt-0.5">Pay in full</div>
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

                <!-- Cash: payment method -->
                <div v-if="currentPlan === 'cash'">
                  <div class="text-[11px] text-gray-400 uppercase tracking-wide mb-2">Payment method</div>
                  <div class="grid grid-cols-3 gap-2">
                    <div v-for="m in ['mpamba', 'airtel', 'visa']" :key="m"
                      class="border rounded-lg p-2.5 text-center cursor-pointer transition-all"
                      :class="currentMethod === m ? 'border-2 border-violet-500 bg-violet-50 dark:bg-violet-950' : 'border-gray-200 dark:border-gray-700'"
                      @click="currentMethod = m as 'mpamba' | 'airtel' | 'visa'">
                      <div class="text-base mb-0.5">{{ m === 'mpamba' ? '📱' : m === 'airtel' ? '📲' : '💳' }}</div>
                      <div class="text-xs font-medium text-gray-700 dark:text-gray-300">
                        {{ m === 'mpamba' ? 'Mpamba' : m === 'airtel' ? 'Airtel' : 'Visa' }}
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Amount summary (cash only) -->
                <div v-if="currentPlan === 'cash'" class="space-y-1 pt-1">
                  <div class="flex justify-between text-xs text-gray-400">
                    <span>System price</span><span>{{ fmt(currentPkg.price) }}</span>
                  </div>
                  <div class="flex justify-between text-sm font-medium text-gray-900 dark:text-white border-t border-gray-100 dark:border-gray-800 pt-2 mt-1">
                    <span>Pay now</span><span>{{ fmt(dueNow(currentPkg)) }}</span>
                  </div>
                </div>

                <button
                  v-if="currentPlan === 'cash'"
                  class="w-full py-3 rounded-lg text-sm font-medium transition-opacity bg-violet-600 text-white hover:opacity-90"
                  @click="proceedCheckout">
                  Continue to payment →
                </button>
              </div>

              <!-- Step: pay -->
              <div v-if="checkoutStep === 'pay' && currentPkg" class="p-5 space-y-4">
                <div class="bg-gray-50 dark:bg-gray-800 rounded-lg px-4 py-3 flex justify-between items-center">
                  <div class="text-sm font-medium text-gray-900 dark:text-white">{{ currentPkg.kva }} KVA — {{ fmt(dueNow(currentPkg)) }}</div>
                  <div class="text-xs text-gray-400">Full payment</div>
                </div>

                <!-- Mobile money form -->
                <template v-if="currentMethod === 'mpamba' || currentMethod === 'airtel'">
                  <div>
                    <label class="text-xs text-gray-400 block mb-1">Mobile number</label>
                    <input v-model="mobileNumber" :placeholder="currentMethod === 'mpamba' ? 'e.g. 0991234567' : 'e.g. 0881234567'"
                      class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 rounded-lg text-sm bg-white dark:bg-gray-800 text-gray-900 dark:text-white outline-none focus:border-violet-500" />
                    <p class="text-[11px] text-gray-400 mt-1">
                      You will receive a prompt on your phone to confirm the payment of {{ fmt(dueNow(currentPkg)) }}.
                    </p>
                  </div>
                </template>

                <!-- Visa card form -->
                <template v-if="currentMethod === 'visa'">
                  <div class="space-y-3">
                    <div>
                      <label class="text-xs text-gray-400 block mb-1">Card number</label>
                      <input :value="cardNumber" placeholder="1234 5678 9012 3456" maxlength="19"
                        class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 rounded-lg text-sm bg-white dark:bg-gray-800 text-gray-900 dark:text-white outline-none focus:border-violet-500"
                        @input="formatCardInput" />
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                      <div>
                        <label class="text-xs text-gray-400 block mb-1">Expiry</label>
                        <input v-model="cardExpiry" placeholder="MM / YY" maxlength="7"
                          class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 rounded-lg text-sm bg-white dark:bg-gray-800 text-gray-900 dark:text-white outline-none focus:border-violet-500" />
                      </div>
                      <div>
                        <label class="text-xs text-gray-400 block mb-1">CVV</label>
                        <input v-model="cardCvv" placeholder="123" maxlength="3" type="password"
                          class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 rounded-lg text-sm bg-white dark:bg-gray-800 text-gray-900 dark:text-white outline-none focus:border-violet-500" />
                      </div>
                    </div>
                    <div>
                      <label class="text-xs text-gray-400 block mb-1">Name on card</label>
                      <input v-model="cardName" placeholder="Full name"
                        class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 rounded-lg text-sm bg-white dark:bg-gray-800 text-gray-900 dark:text-white outline-none focus:border-violet-500" />
                    </div>
                  </div>
                </template>

                <button
                  class="w-full py-3 rounded-lg bg-violet-600 text-white text-sm font-medium hover:opacity-90 transition-opacity"
                  @click="confirmPayment">
                  Confirm — {{ fmt(dueNow(currentPkg)) }}
                </button>
              </div>

              <!-- Step: success -->
              <div v-if="checkoutStep === 'success' && currentPkg" class="p-6 text-center space-y-3">
                <div class="w-12 h-12 rounded-full bg-green-100 dark:bg-green-900 flex items-center justify-center mx-auto text-green-600 dark:text-green-300 text-xl">✓</div>
                <div class="text-base font-medium text-gray-900 dark:text-white">Payment initiated!</div>
                <div class="text-sm text-gray-500 dark:text-gray-400 leading-relaxed">
                  Your <strong>{{ currentPkg.kva }} KVA solar system</strong> order has been received.<br />
                  <strong>{{ fmt(dueNow(currentPkg)) }}</strong> will be processed via
                  <strong>{{ methodLabels[currentMethod] }}</strong>.<br /><br />
                  Our team will contact you within 24 hours to confirm your delivery.
                </div>
                <a href="https://wa.me/265886616931" target="_blank"
                  class="inline-flex items-center gap-2 mt-1 bg-green-500 text-white text-sm px-5 py-2.5 rounded-full hover:bg-green-600 transition-colors no-underline">
                  Chat on WhatsApp
                </a>
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