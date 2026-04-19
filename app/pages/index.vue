<script setup lang="ts">
import { ref } from 'vue'

const { isNotificationsSlideoverOpen } = useDashboard()

const products = [
  {
    kva: 3,
    price: 7900000,
    tag: null,
    desc: 'Ideal for a small home. Powers lights, fans, phone charging, a TV and a small fridge.',
    specs: ['Lithium battery', 'Solar panels', 'MUST inverter', 'Installation kit'],
    color: '#1D9E75',
  },
  {
    kva: 5,
    price: 9950000,
    tag: null,
    desc: 'Perfect for a medium home. Handles lighting, entertainment, fridge and a small water pump.',
    specs: ['Lithium battery', 'Solar panels', 'MUST inverter', 'MPPT controller'],
    color: '#378ADD',
  },
  {
    kva: 6,
    price: 10900000,
    tag: 'Most popular',
    desc: 'Our best-seller. Comfortably runs a full household — fridge, TV, lights, fans and more.',
    specs: ['LiFePO4 battery', 'High-yield panels', 'MUST inverter', 'MPPT controller'],
    color: '#534AB7',
  },
  {
    kva: 12,
    price: 16900000,
    tag: null,
    desc: 'Large family home or small office. Supports air conditioning, computers and heavy appliances.',
    specs: ['LiFePO4 battery', 'Dual panel array', 'MUST inverter', 'Smart controller'],
    color: '#D85A30',
  },
  {
    kva: 20,
    price: 35000000,
    tag: null,
    desc: 'Small to medium business. Handles multiple workstations, printers, fridges and security systems.',
    specs: ['Commercial battery', 'Large panel array', '3-phase inverter', 'Monitoring system'],
    color: '#BA7517',
  },
  {
    kva: 60,
    price: 68000000,
    tag: null,
    desc: 'Medium enterprise. Powers full offices, workshops or lodges with heavy equipment.',
    specs: ['Industrial batteries', 'Commercial panels', 'Industrial inverter', 'Remote monitoring'],
    color: '#185FA5',
  },
  {
    kva: 100,
    price: 92000000,
    tag: null,
    desc: 'Large commercial or industrial. Complete off-grid independence for factories and large facilities.',
    specs: ['Industrial battery bank', 'Large-scale panels', 'Industrial inverter', 'Full BMS system'],
    color: '#993C1D',
  },
]

const fmt = (n: number) => 'MWK ' + n.toLocaleString()

// Modal state
const modalOpen = ref(false)
const currentPkg = ref<(typeof products)[0] | null>(null)
const currentPlan = ref<'full' | 'installment'>('full')
const currentMethod = ref<'mpamba' | 'airtel' | 'visa' | null>(null)
const checkoutStep = ref<'select' | 'pay' | 'success'>('select')

// Pay form fields
const mobileNumber = ref('')
const cardNumber = ref('')
const cardExpiry = ref('')
const cardCvv = ref('')
const cardName = ref('')

function openModal(pkg: (typeof products)[0]) {
  currentPkg.value = pkg
  currentPlan.value = 'full'
  currentMethod.value = null
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
  const dep = Math.round(pkg.price * 0.3)
  return currentPlan.value === 'full' ? pkg.price : dep
}

function balance(pkg: (typeof products)[0]) {
  return pkg.price - Math.round(pkg.price * 0.3)
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

        <!-- Brand header -->
        <div class="flex items-center justify-between flex-wrap gap-4">
          <div class="flex items-center gap-3">
            <div
              class="w-10 h-10 rounded-full bg-violet-600 flex items-center justify-center text-white font-medium text-sm">
              S
            </div>
            <div>
              <UToggle />
              <div class="text-base font-medium text-gray-900 dark:text-white">OTG 4 U</div>
              <div class="text-xs text-gray-400 uppercase tracking-widest">Ignite your future</div>
            </div>
          </div>
          <div class="flex text-xs items-center text-gray-400 gap-4">
            <div class="flex gap-2">
              <UColorModeSwitch />
            </div>
            <p>Blantyre · Lilongwe · Mzuzu · Karonga</p>
          </div>
        </div>

        <!-- Hero section -->
        <div
          class="relative overflow-hidden rounded-2xl border border-violet-100 dark:border-violet-900 bg-gradient-to-br from-violet-50 via-white to-violet-100 dark:from-violet-950 dark:via-gray-900 dark:to-violet-900 p-6 md:p-10">

          <!-- Background glow -->
          <div class="absolute -top-20 -right-20 w-72 h-72 bg-violet-400/20 rounded-full blur-3xl"></div>
          <div class="absolute -bottom-20 -left-20 w-72 h-72 bg-indigo-400/20 rounded-full blur-3xl"></div>

          <div class="relative flex flex-col lg:flex-row items-start lg:items-center justify-between gap-8">

            <!-- Left content -->
            <div class="max-w-xl">
              <h1 class="text-2xl md:text-3xl font-semibold text-gray-900 dark:text-white leading-tight">
                Power Your Home with
                <span class="text-violet-600">Reliable Solar Energy</span>
              </h1>

              <p class="mt-3 text-sm md:text-base text-gray-600 dark:text-gray-400 leading-relaxed">
                Complete off-grid solar systems designed for Malawi. From small homes to large businesses —
                clean, reliable power with flexible payment options.
              </p>

              <!-- Highlights -->
              <div class="flex flex-wrap gap-2 mt-4">
                <span
                  class="text-xs px-3 py-1 rounded-full bg-violet-100 dark:bg-violet-900 text-violet-700 dark:text-violet-300">
                  ⚡ No ESCOM outages
                </span>
                <span
                  class="text-xs px-3 py-1 rounded-full bg-violet-100 dark:bg-violet-900 text-violet-700 dark:text-violet-300">
                  💳 30% deposit available
                </span>
                <span
                  class="text-xs px-3 py-1 rounded-full bg-violet-100 dark:bg-violet-900 text-violet-700 dark:text-violet-300">
                  🔧 Installation included
                </span>
              </div>

              <!-- CTA -->
              <div class="flex flex-wrap gap-3 mt-6">
                <button
                  class="px-5 py-3 rounded-lg bg-violet-600 text-white text-sm font-medium hover:opacity-90 transition">
                  Browse Systems
                </button>

                <a href="https://wa.me/265995441381" target="_blank"
                  class="px-5 py-3 rounded-lg border border-gray-200 dark:border-gray-700 text-sm text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-gray-800 transition">
                  Talk to Sales
                </a>
              </div>
            </div>

            <!-- Right visual -->
            <div class="flex-1 flex justify-center lg:justify-end">
              <div class="grid grid-cols-2 gap-3 max-w-xs">

                <!-- Mini cards -->
                <div
                  class="rounded-xl p-3 bg-white/70 dark:bg-gray-800/70 border border-gray-200 dark:border-gray-700 backdrop-blur">
                  <div class="text-xs text-gray-400">Starting from</div>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white">3 KVA</div>
                </div>

                <div
                  class="rounded-xl p-3 bg-white/70 dark:bg-gray-800/70 border border-gray-200 dark:border-gray-700 backdrop-blur">
                  <div class="text-xs text-gray-400">Max capacity</div>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white">100 KVA</div>
                </div>

                <div
                  class="rounded-xl p-3 bg-white/70 dark:bg-gray-800/70 border border-gray-200 dark:border-gray-700 backdrop-blur">
                  <div class="text-xs text-gray-400">Coverage</div>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white">Nationwide</div>
                </div>

                <div
                  class="rounded-xl p-3 bg-white/70 dark:bg-gray-800/70 border border-gray-200 dark:border-gray-700 backdrop-blur">
                  <div class="text-xs text-gray-400">Install time</div>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white">2–5 days</div>
                </div>

              </div>
            </div>

          </div>
        </div>

        <!-- Product grid -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
          <div v-for="pkg in products" :key="pkg.kva"
            class="rounded-xl border border-gray-200 dark:border-gray-700 bg-white dark:bg-gray-900 flex flex-col overflow-hidden">
            <!-- Product image area -->
            <div class="h-36 flex items-center justify-center relative" :style="{ background: pkg.color + '18' }">
              <span v-if="pkg.tag" class="absolute top-2 left-2 text-[10px] px-2 py-0.5 rounded-full text-white"
                :style="{ background: pkg.color }">
                {{ pkg.tag }}
              </span>
              <!-- Panel illustration SVG -->
              <svg viewBox="0 0 80 80" class="w-20 h-20 opacity-85" xmlns="http://www.w3.org/2000/svg">
                <rect x="4" y="28" width="72" height="44" rx="3" :fill="pkg.color" opacity="0.15" />
                <rect x="4" y="28" width="72" height="44" rx="3" fill="none" :stroke="pkg.color" stroke-width="1.5" />
                <line x1="28" y1="28" x2="28" y2="72" :stroke="pkg.color" stroke-width="1" opacity="0.5" />
                <line x1="52" y1="28" x2="52" y2="72" :stroke="pkg.color" stroke-width="1" opacity="0.5" />
                <line x1="4" y1="44" x2="76" y2="44" :stroke="pkg.color" stroke-width="1" opacity="0.5" />
                <line x1="4" y1="58" x2="76" y2="58" :stroke="pkg.color" stroke-width="1" opacity="0.5" />
                <rect x="22" y="6" width="36" height="22" rx="3" :fill="pkg.color" opacity="0.2" />
                <rect x="22" y="6" width="36" height="22" rx="3" fill="none" :stroke="pkg.color" stroke-width="1.5" />
                <rect x="32" y="8" width="16" height="8" rx="1.5" :fill="pkg.color" opacity="0.4" />
                <rect x="32" y="18" width="16" height="8" rx="1.5" :fill="pkg.color" opacity="0.4" />
                <rect x="36" y="28" width="8" height="6" rx="1" :fill="pkg.color" opacity="0.7" />
                <rect x="10" y="42" width="14" height="24" rx="2" :fill="pkg.color" opacity="0.25" />
                <rect x="10" y="42" width="14" height="24" rx="2" fill="none" :stroke="pkg.color" stroke-width="1" />
                <rect x="12" y="44" width="10" height="4" rx="1" :fill="pkg.color" opacity="0.5" />
                <rect x="12" y="50" width="10" height="4" rx="1" :fill="pkg.color" opacity="0.5" />
                <rect x="12" y="56" width="10" height="4" rx="1" :fill="pkg.color" opacity="0.5" />
              </svg>
            </div>

            <!-- Card body -->
            <div class="p-3 flex flex-col gap-1.5 flex-1">
              <div class="text-xl font-medium" :style="{ color: pkg.color }">{{ pkg.kva }} KVA</div>
              <div class="text-xs text-gray-400">Complete solar system</div>
              <div class="text-xs text-gray-500 dark:text-gray-400 leading-relaxed flex-1">{{ pkg.desc }}</div>
              <div class="flex flex-wrap gap-1 mt-1">
                <span v-for="spec in pkg.specs" :key="spec"
                  class="text-[10px] bg-gray-100 dark:bg-gray-800 text-gray-500 dark:text-gray-400 px-2 py-0.5 rounded">
                  {{ spec }}
                </span>
              </div>
              <div class="text-sm font-medium text-gray-900 dark:text-white mt-1">{{ fmt(pkg.price) }}</div>
              <div class="text-xs text-gray-400">Deposit from {{ fmt(Math.round(pkg.price * 0.3)) }}</div>
            </div>

            <button
              class="mx-3 mb-3 py-2.5 rounded-lg text-white text-sm font-medium transition-opacity hover:opacity-85"
              :style="{ background: pkg.color }" @click="openModal(pkg)">
              Buy now
            </button>
          </div>
        </div>
      </div>

      <!-- Buy Modal -->
      <Teleport to="body">
        <Transition name="fade">
          <div v-if="modalOpen" class="fixed inset-0 z-50 flex items-center justify-center bg-black/45"
            @click.self="closeModal">
            <div
              class="bg-white dark:bg-gray-900 rounded-xl border border-gray-200 dark:border-gray-700 w-full max-w-md mx-4 overflow-hidden">

              <!-- Modal header -->
              <div class="flex items-center justify-between px-5 py-4 border-b border-gray-100 dark:border-gray-800">
                <span class="text-sm font-medium text-gray-900 dark:text-white">
                  <template v-if="checkoutStep === 'success'">Order confirmed</template>
                  <template v-else>Buy {{ currentPkg?.kva }} KVA system</template>
                </span>
                <button class="text-gray-400 hover:text-gray-600 text-lg leading-none px-1"
                  @click="closeModal">✕</button>
              </div>

              <!-- Step: select plan + method -->
              <div v-if="checkoutStep === 'select' && currentPkg" class="p-5 space-y-4">
                <div class="bg-gray-50 dark:bg-gray-800 rounded-lg px-4 py-3 flex justify-between items-center">
                  <div class="text-sm font-medium text-gray-900 dark:text-white">{{ currentPkg.kva }} KVA solar system
                  </div>
                  <div class="text-sm text-gray-500">{{ fmt(currentPkg.price) }}</div>
                </div>

                <div>
                  <div class="text-[11px] text-gray-400 uppercase tracking-wide mb-2">Payment plan</div>
                  <div class="grid grid-cols-2 gap-2">
                    <div class="border rounded-lg p-3 text-center cursor-pointer transition-all"
                      :class="currentPlan === 'full' ? 'border-2 border-violet-500 bg-violet-50 dark:bg-violet-950' : 'border-gray-200 dark:border-gray-700'"
                      @click="currentPlan = 'full'">
                      <div class="text-xs font-medium text-gray-800 dark:text-gray-200">Full payment</div>
                      <div class="text-[11px] text-gray-400 mt-0.5">{{ fmt(currentPkg.price) }}</div>
                    </div>
                    <a href="https://swiftcapital.mw/apply-for-a-loan/" <div
                      class="border rounded-lg p-3 text-center cursor-pointer transition-all"
                      :class="currentPlan === 'installment' ? 'border-2 border-violet-500 bg-violet-50 dark:bg-violet-950' : 'border-gray-200 dark:border-gray-700'"
                      @click="currentPlan = 'installment'">
                      <div class="text-xs font-medium text-gray-800 dark:text-gray-200">Swift Capital</div>
                      <div class="text-[11px] text-gray-400 mt-0.5">30% — {{ fmt(Math.round(currentPkg.price * 0.3)) }}
                      </div>
                    </a>
                  </div>
                </div>
              </div>

              <div>
                <div class="text-[11px] text-gray-400 uppercase tracking-wide mb-2">Pay with</div>
                <div class="space-y-2">
                  <div class="flex-1">
                    <div class="text-sm font-medium text-gray-800 dark:text-gray-200">
                      {{ m === 'Swift Capital' ? 'Swift Capital' : m === 'VISA' ? 'VISA' : 'VISA' }}
                    </div>
                    <div class="text-[11px] text-gray-400">
                      {{ m === 'Swift Capital' ? 'Swift Capital' : m === 'VISA' ? 'VISA' : 'VISA' }}
                    </div>
                  </div>
                  <div class="w-4 h-4 rounded-full border flex items-center justify-center shrink-0"
                    :class="currentMethod === m ? 'bg-violet-600 border-violet-600' : 'border-gray-300 dark:border-gray-600'">
                    <div v-if="currentMethod === m" class="w-1.5 h-1.5 rounded-full bg-white" />
                  </div>
                </div>
              </div>
            </div>

            <!-- Amount summary -->
            <div class="space-y-1 pt-1">
              <div class="flex justify-between text-xs text-gray-400">
                <span>System price</span><span>{{ fmt(currentPkg.price) }}</span>
              </div>
              <div v-if="currentPlan === 'installment'" class="flex justify-between text-xs text-gray-400">
                <span>Balance on delivery</span><span>{{ fmt(balance(currentPkg)) }}</span>
              </div>
              <div
                class="flex justify-between text-sm font-medium text-gray-900 dark:text-white border-t border-gray-100 dark:border-gray-800 pt-2 mt-1">
                <span>Pay now</span><span>{{ fmt(dueNow(currentPkg)) }}</span>
              </div>
            </div>

            <button class="w-full py-3 rounded-lg text-sm font-medium transition-opacity"
              :class="currentMethod ? 'bg-violet-600 text-white hover:opacity-90' : 'bg-gray-200 dark:bg-gray-700 text-gray-400 cursor-not-allowed'"
              :disabled="!currentMethod" @click="proceedCheckout">
              {{ currentMethod ? 'Continue to payment →' : 'Select a payment method' }}
            </button>
          </div>

          <!-- Step: pay -->
          <div v-if="checkoutStep === 'pay' && currentPkg" class="p-5 space-y-4">
            <div class="bg-gray-50 dark:bg-gray-800 rounded-lg px-4 py-3 flex justify-between items-center">
              <div class="text-sm font-medium text-gray-900 dark:text-white">{{ currentPkg.kva }} KVA — {{
                fmt(dueNow(currentPkg))
              }}</div>
              <div class="text-xs text-gray-400">{{ currentPlan === 'installment' ? '30% deposit' : 'Full payment' }}
              </div>
            </div>

            <!-- Visa card form -->
            <template>
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
            <div
              class="w-12 h-12 rounded-full bg-green-100 dark:bg-green-900 flex items-center justify-center mx-auto text-green-600 dark:text-green-300 text-xl">
              ✓
            </div>
            <div class="text-base font-medium text-gray-900 dark:text-white">Payment initiated!</div>
            <div class="text-sm text-gray-500 dark:text-gray-400 leading-relaxed">
              Your <strong>{{ currentPkg.kva }} KVA solar system</strong> order has been received.<br />
              <strong>{{ fmt(dueNow(currentPkg)) }}</strong> will be processed via
              <strong>{{ methodLabels[currentMethod!] }}</strong>.<br /><br />
              Our team will contact you within 24 hours to confirm your delivery.
            </div>
            <a href="https://wa.me/265995441381" target="_blank"
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