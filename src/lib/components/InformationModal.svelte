<script>
  import { surah, ayah } from "../store";
  import { quran } from "../values/quran_summerizing";
</script>

<input type="checkbox" id="information-modal" class="modal-toggle" />
<label  dir="rtl" for="information-modal" class="modal cursor-pointer">
  <label class="modal-box relative" for="">
    <h3 class="text-lg font-bold">
      سورة {quran[$surah]["name_translations"]["ar"]}
    </h3>
    <h3 class="text-lg font-bold">الاية</h3>
    <p class="py-4">{$ayah + 1} / {quran[$surah]["ayah_before"] + $ayah + 1} </p>
    <h3 class="text-lg font-bold">المقرئ</h3>
    <p class="py-4">مشاري راشد العفاسي</p>
    <h3 class="text-lg font-bold">التفسير</h3>
    <p class="py-4">التفسير الميسر</p>
  </label>
</label>
