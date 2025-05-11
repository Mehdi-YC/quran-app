<script>
  import { surah } from "../store";
  import { quran } from "../values/quran_summerizing";

  export let tafsir_nb;
  export let tafsir_txt;

  let showModal = false;
</script>

<!-- Trigger Button or Interaction -->
<button class="btn btn-primary" onclick={() => (showModal = true)}>
Show Tafsir
</button>

<!-- Modal -->
{#if showModal}
<div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
  <div class="bg-background rounded-lg p-6 max-w-md w-full shadow-lg relative">
    <button
      class="absolute top-2 left-2 text-xl"
      onclick={() => (showModal = false)}
    >
      ✕
    </button>

    <h3 class="text-lg font-bold mb-2">
      {quran[$surah].name_translations.ar} - {tafsir_nb + 1}
    </h3>

    <p class="py-4">{tafsir_txt}</p>
  </div>
</div>
{/if}
