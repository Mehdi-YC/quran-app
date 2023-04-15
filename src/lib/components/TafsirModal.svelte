
<script>
    import { surah } from "../store";
    import { quran } from "../values/quran_summerizing";
    export let tafsir_nb;
    export let tafsir_txt;
</script>


<input type="checkbox" id="tafsir-modal" class="modal-toggle" />
<label for="tafsir-modal" class="modal cursor-pointer">
  <label class="modal-box relative" for="">
    <h3 class="text-lg font-bold">{quran[$surah+1].name_translations.ar}-{tafsir_nb}</h3>
    <p class="py-4">{tafsir_txt}</p>
  </label>
</label>