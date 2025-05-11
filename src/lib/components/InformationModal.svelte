<script>
  import { surah, ayah } from "../store";
  import { quran } from "../values/quran_summerizing";

  let showModal = true;
  function toggleModal(){
    showModal = !showModal
  }
</script>

<!-- Trigger Button -->
<button onclick={toggleModal} class="btn btn-primary" style="z-index:100">
  Show Information
</button>

<!-- Modal -->
{#if showModal}
  <div class="fixed inset-0 flex items-center justify-center  bg-opacity-50 z-50">
    <div dir="rtl" class="bg-background rounded-lg p-6 max-w-md w-full shadow-lg relative">
      <button
        class="absolute top-2 left-2 text-xl"
        onclick={toggleModal}
      >
        ✕
      </button>

      <h3 class="text-lg font-bold mb-2">
        سورة {quran[$surah]["name_translations"]["ar"]}
      </h3>

      <h3 class="text-lg font-bold">الاية</h3>
      <p class="py-2">
        {$ayah + 1} / {quran[$surah]["ayah_before"] + $ayah + 1}
      </p>

      <h3 class="text-lg font-bold">المقرئ</h3>
      <p class="py-2">مشاري راشد العفاسي</p>

      <h3 class="text-lg font-bold">التفسير</h3>
      <p class="py-2">التفسير الميسر</p>
    </div>
  </div>
{/if}
