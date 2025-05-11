<script>
  import { surah } from "../store";
  import { quran } from "../values/quran_summerizing";

  let { tafsir_nb, tafsir_txt, show_tafsir = $bindable() } = $props();

</script>

<!-- Modal -->
{#if show_tafsir}
  <div
    class=" fixed inset-0 flex items-center justify-center z-50 mx-2"
    style="top:50px"
  >
    <div class="bg-surface-800 rounded-lg p-6 max-w-md w-full shadow-lg relative">
      <button
        class="absolute top-2 left-2 text-xl"
        onclick={() => (show_tafsir = false)}
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
