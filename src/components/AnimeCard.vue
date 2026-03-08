<script setup>
import { computed, ref, watch } from 'vue'

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

const emit = defineEmits(['add'])
const synopsisExpanded = ref(false)
const animeImage = computed(() => {
  return (
    props.anime?.image?.jpg?.large_image_url ||
    props.anime?.image?.jpg?.image_url ||
    props.anime?.image?.webp?.large_image_url ||
    props.anime?.image?.webp?.image_url ||
    ''
  )
})
const synopsis = computed(() => {
  return props.anime?.synopsis || 'Synopsis not available.'
})
const needsTruncation = computed(() => synopsis.value.length > 240)
const visibleSynopsis = computed(() => {
  if (synopsisExpanded.value || !needsTruncation.value) {
    return synopsis.value
  }
  return `${synopsis.value.slice(0, 240)}...`
})
watch(
  () => props.anime?.mal_id,
  () => {
    synopsisExpanded.value = false
  },
)
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
    <div
      v-else-if="error"
      class="rounded-lg border border-pink-800 bg-pink-400/10 p-4 text-sm text-pink-600"
    >
      <h3 class="text-lg font-semibold">Failed to Load Anime</h3>
      <p class="mt-2 text-sm text-slate-400/90">{{ error }}</p>
    </div>
    <div
      v-else-if="anime"
      class="space-y-4"
    >
      <div class="overflow-hidden rounded-2xl border border-slate-700/70 bg-slate-800/70">
        <img
          v-if="animeImage"
          :src="animeImage"
          :alt="anime.title"
          class="bg-slae-900/50 h-88 w-full object-contain"
          loading="lazy"
        />
        <div
          v-else
          class="flex h-88 items-center justify-center bg-slate-900/50 text-slate-400"
        >
          No Image Available
        </div>
      </div>

      <div>
        <h2 class="text-2sl font-black text-purple-600">{{ anime.title }}</h2>
        <p class="mt-2 text-sm text-slate-400">
          Score: <span class="font-semibold text-pink-400">{{ anime.score ?? 'N/A' }}</span> .
          Episodes:
          <span class="font-semibold text-purple-400">{{ anime.episodes ?? 'N/A' }}</span> . Rating:
          <span class="font-semibold text-yellow-500">{{ anime.rating ?? 'N/A' }}</span>
        </p>
      </div>

      <p class="loading-relaxed text-sm text-slate-200">
        {{ visibleSynopsis }}
        <button
          v-if="needsTruncation"
          type="button"
          class="ml-2 text-pink-400 underline-offset-4 hover:underline"
          @click="synopsisExpanded = !synopsisExpanded"
        >
          {{ synopsisExpanded ? 'Show Less' : 'Read More' }}
        </button>
      </p>

      <div class="flex flex-wrap gap-3">
        <button
          type="button"
          class="bg-purple-900-15 teste-sm rounded-full border border-purple-500/70 px-4 py-2 font-semibold text-purple-200"
          :disabled="inWatchlist"
          @click="emit('add', anime)"
        >
          {{ inWatchlist ? 'In Watchlist' : 'Add to Watchlist' }}
        </button>

        <a
          :href="anime.url"
          target="_blank"
          rel="noopener noreferrer"
          class="rounded-full border border-pink-500/70 bg-pink-900/15 px-4 py-2 text-sm font-semibold text-pink-200 hover:bg-pink-600/20"
        >
          Open on MAL
        </a>
      </div>
    </div>
    <div
      v-else
      class="rounded-2xl border border-slate-700/60 bg-slate-800/40 p-6 text-center text-pink-400"
    >
      SPIN TO WIN!...a new anime recommendation...
    </div>
  </section>
</template>
