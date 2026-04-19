<template>
  <nav>

  </nav>
  <slot/>
  <!-- Footer -->
<div class="mt-10 border-t border-gray-200 dark:border-gray-800 pt-6 pb-4 px-2">

  <div class="flex flex-col md:flex-row items-start md:items-center justify-between gap-6">

    <!-- Brand -->
    <div class="flex items-center gap-3">
      <div class="w-9 h-9 rounded-full bg-violet-600 flex items-center justify-center text-white text-sm font-medium">
        OTG
      </div>
      <div>
        <div class="text-sm font-medium text-gray-900 dark:text-white">
          OTG 4 U
        </div>
        <div class="text-xs text-gray-400 tracking-wide">
          Ignite your future
        </div>
      </div>
    </div>

    <!-- Links -->
    <div class="flex flex-wrap gap-4 text-xs text-gray-500 dark:text-gray-400">
      <a href="#" class="hover:text-violet-600 transition">Products</a>
      <a href="#" class="hover:text-violet-600 transition">Installations</a>
      <a href="#" class="hover:text-violet-600 transition">Support</a>
      <a href="#" class="hover:text-violet-600 transition">Contact</a>
    </div>

    <!-- Contact -->
    <div class="text-xs text-gray-400">
      <div>Blantyre · Lilongwe · Mzuzu · Karonga</div>
      <div class="mt-1">+265 995 441 381</div>
    </div>

  </div>

  <!-- Bottom bar -->
  <div class="mt-6 flex flex-col md:flex-row items-center justify-between gap-3 border-t border-gray-100 dark:border-gray-800 pt-4">

    <div class="text-[11px] text-gray-400">
      © {{ new Date().getFullYear() }} OTG 4 U. All rights reserved.
    </div>

    <div class="text-[11px] text-gray-400">
      Powered by <span class="text-violet-600 font-medium">OTG</span>
    </div>

  </div>

</div>
</template>
