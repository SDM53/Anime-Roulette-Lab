<script setup>
import { useMouse } from '@vueuse/core'

const { x, y, sourceType } = useMouse()
</script>

<template>
  <main
    class="min-h-screen bg-[radial-gradient(circle_at_89%_5%,#fc3294,transparent_32%),radial-gradient(circle_at_20%_60%,#9031b5,transparent_61%),linear-gradient(180deg,#0e1929,#030a14,#000205)] px-4 py-8 text-slate-100 sm:px-6 lg:px-8"
  >
    <div class="mx-auto max-w-7xl">
      <header>
        <p class="text-sx font-semi-bold tracking-[0.3em] text-pink-500 uppercase">Project #4</p>
        <h1 class="mt-2 text-7xl font-black text-purple-600 sm:text-6xl">Anime RNG</h1>
        <p class="mt-2 max-w-3xl text-sm text-slate-400 sm:text-base">
          Spin the reel, request a random anime from Jinkan with VueUSe useFech, and learnhow REST
          APIs signal rate limiting with HTTP 429.
        </p>
      </header>
    </div>
  </main>
</template>
