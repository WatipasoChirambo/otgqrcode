<script setup lang="ts">
const products = [
  {
    kva: 3,
    price: 7900000,
    desc: 'Ideal for a small home. Powers lights, fans, phone charging, a TV and a small fridge.',
    specs: ['Lithium battery', 'Solar panels', 'MUST inverter', 'Installation kit'],
    color: '#1D9E75',
  },
  {
    kva: 5,
    price: 9950000,
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
    desc: 'Large family home or small office. Supports air conditioning, computers and heavy appliances.',
    specs: ['LiFePO4 battery', 'Dual panel array', 'MUST inverter', 'Smart controller'],
    color: '#D85A30',
  },
  {
    kva: 20,
    price: 35000000,
    desc: 'Small to medium business. Handles multiple workstations, printers, fridges and security systems.',
    specs: ['Commercial battery', 'Large panel array', '3-phase inverter', 'Monitoring system'],
    color: '#BA7517',
  },
  {
    kva: 60,
    price: 68000000,
    desc: 'Medium enterprise. Powers full offices, workshops or lodges with heavy equipment.',
    specs: ['Industrial batteries', 'Commercial panels', 'Industrial inverter', 'Remote monitoring'],
    color: '#185FA5',
  },
  {
    kva: 100,
    price: 92000000,
    desc: 'Large commercial or industrial. Complete off-grid independence for factories and large facilities.',
    specs: ['Industrial battery bank', 'Large-scale panels', 'Industrial inverter', 'Full BMS system'],
    color: '#993C1D',
  },
]

const fmt = (n: number) => 'MWK ' + n.toLocaleString()
</script>

<template>
  <UDashboardPanel id="solar-systems">
    <template #body>
      <div class="p-6 space-y-6">

        <!-- Header -->
        <div class="flex items-center justify-between gap-4">
          <div>
            <img src="/logo.jpg" height="170px" width="170px"/>
          </div>

          <div>
            <a
            href="tel:+0886616931"
            class="px-5 py-3 rounded-lg bg-violet-600 text-white text-sm font-medium hover:opacity-90 transition"
          >
            📞 Sales
          </a>
          </div>
          
        </div>

        <!-- Hero -->
        <div class="rounded-2xl p-6 bg-gradient-to-br from-violet-50 to-white dark:from-violet-950 dark:to-gray-900 border border-violet-100 dark:border-violet-900">
          <h1 class="text-2xl font-semibold text-gray-900 dark:text-white">
            Reliable Solar Power for Every Home
          </h1>
          <p class="text-sm text-gray-500 mt-2">
            Browse systems below and call us instantly to order or get advice.
          </p>
        </div>

        <!-- Products -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
          <div
            v-for="pkg in products"
            :key="pkg.kva"
            class="rounded-xl border border-gray-200 dark:border-gray-700 bg-white dark:bg-gray-900 overflow-hidden flex flex-col"
          >

            <!-- Top -->
            <div
              class="h-36 flex items-center justify-center relative"
              :style="{ background: pkg.color + '18' }"
            >
              <span
                v-if="pkg.tag"
                class="absolute top-2 left-2 text-[10px] px-2 py-0.5 rounded-full text-white"
                :style="{ background: pkg.color }"
              >
                {{ pkg.tag }}
              </span>

              <div class="text-2xl font-semibold" :style="{ color: pkg.color }">
                {{ pkg.kva }} KVA
              </div>
            </div>

            <!-- Body -->
            <div class="p-3 flex flex-col gap-2 flex-1">
              <div class="text-xs text-gray-400">Complete solar system</div>

              <div class="text-xs text-gray-500 dark:text-gray-400 flex-1">
                {{ pkg.desc }}
              </div>

              <div class="flex flex-wrap gap-1">
                <span
                  v-for="spec in pkg.specs"
                  :key="spec"
                  class="text-[10px] bg-gray-100 dark:bg-gray-800 text-gray-500 px-2 py-0.5 rounded"
                >
                  {{ spec }}
                </span>
              </div>

              <div class="text-sm font-medium text-gray-900 dark:text-white mt-1">
                {{ fmt(pkg.price) }}
              </div>
            </div>

            <!-- Call button -->
            <a
              href="tel:+0886616931"
              class="mx-3 mb-3 py-2.5 rounded-lg text-white text-sm font-medium text-center transition"
              :style="{ background: pkg.color }"
            >
              Talk to Sales
            </a>

          </div>
        </div>

        <!-- Footer CTA -->
        <div class="text-center pt-6">
          <div class="text-sm text-gray-500 mb-3">
            Need help choosing the right system?
          </div>

          <a
            href="tel:+0886616931"
            class="inline-block px-6 py-3 rounded-full bg-violet-600 text-white text-sm font-medium hover:opacity-90"
          >
            Call Now: +0886616931
          </a>
        </div>

      </div>
    </template>
  </UDashboardPanel>
</template>