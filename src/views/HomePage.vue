<script setup>
import AnimeCard from '@/components/AnimeCard.vue'
const spin = () => console.log('Hello')
</script>

<template>
  <main
    class="min-h-screen bg-[radial-gradient(circle_at_89%_5%,#fc3294,transparent_32%),radial-gradient(circle_at_20%_60%,#9031b5,transparent_61%),linear-gradient(180deg,#0e1929,#030a14,#000205)] px-4 py-8 text-slate-100 sm:px-6 lg:px-8"
  >
    <div class="mx-auto max-w-7xl">
      <header class="mb-9">
        <p class="text-sx font-semi-bold tracking-[0.3em] text-pink-500 uppercase">Project #4</p>
        <h1 class="mt-2 text-7xl font-black text-purple-600 sm:text-6xl">Anime RNG</h1>
        <p class="mt-2 max-w-3xl text-sm text-slate-400 sm:text-base">
          Spin the reel, request a random anime from Jinkan with VueUSe useFech, and learnhow REST
          APIs signal rate limiting with HTTP 429.
        </p>
      </header>

      <div class="grid gap-6 lg:grid-cols-[1.2fr_0.8fr]">
        <selection class="space-y-5">
          <div
            class="rounded-3xl border border-slate-600/70 bg-slate-900/50 p-5 shadow-2xl shadow-slate-950"
          >
            <div class="flex flex-col gap-3 sm:flex-row sm:justify-between">
              <div>
                <h2 class="text-xl font-bold text-purple-600">RNG</h2>
                <p class="text-sm text-slate-400">Pull lever and get an anime!</p>
              </div>
              <button
                type="button"
                class="rounded-full border border-purple-600 bg-slate-800/60 px-6 py-3 text-base font-black tracking-wide text-slate-300 hover:bg-pink-600"
                @click="spin"
              >
                RNJesus Give Me An Anime!
              </button>
            </div>
          </div>
        </selection>

        <AnimeCard loading />
      </div>
    </div>
  </main>
</template>
