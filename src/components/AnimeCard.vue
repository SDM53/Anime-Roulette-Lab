<script setup>
const props = defineProps({
  anime: {
    type: Object,
    defualt: null,
  },
  loading: {
    type: Boolean,
    default: false,
  },
  error: {
    type: String,
    default: '',
  },
  inWatchlist: {
    type: Boolean,
    default: false,
  },
})
</script>

<template>
  <section
    class="rounded-3xl border border-slate-600/70 bg-slate-900/50 p-5 shadow-2xl shadow-slate-950"
  >
    <div
      v-if="loading"
      class="space-y-4"
    >
      <div class="flex items-center gap-3 text-slate-300">
        <div
          class="h-5 w-5 animate-spin rounded-full border-2 border-pink-500 border-t-transparent"
        ></div>
        <p class="font-semibold tracking-wide">Shuffling anime reels...</p>
      </div>

      <div class="grid grid-cols-3 gap-2">
        <div class="animate-pluse h-3 rounded-full bg-slate-700"></div>
        <div class="animate-pluse h-3 rounded-full bg-slate-700"></div>
        <div class="animate-pluse h-3 rounded-full bg-slate-700"></div>
      </div>
      <div class="h-72 animate-pulse rounded-2xl bg-slate-800"></div>
    </div>
    <div v-else>Done!</div>
  </section>
</template>
