<script>
  import BottomBar from "$lib/components/BottomBar.svelte";
  import NavBar from "$lib/components/NavBar.svelte";
  import Surah from "$lib/components/Surah.svelte";
  import InformationModal from "$lib/components/InformationModal.svelte";
  import { quran } from "$lib/values/quran_summerizing";
  import { tafsir } from "$lib/values/tafsir";
  import { surah, ayah } from "$lib/store";

  let current_surah_audio = $state();
  let tafsir_nb = $state(0);
  let tafsir_id_rev = $state();
  let tafsir_txt= $state();

  let verses = $derived(quran[$surah]["verses"]);
  let nb_ayats = $derived(quran[$surah]["n_of_ayah"]);
  let ayat_before = $derived(quran[$surah]["ayah_before"]);
  let current_surah_ar_name = $derived(quran[$surah]["name_translations"]["ar"]);

  function tafsir_update(i) {
    tafsir_nb = i;
    tafsir_id_rev = nb_ayats - 1 - tafsir_nb;
    tafsir_txt = tafsir[$surah][tafsir_id_rev]["text"];
  }

  //audio
  let audio;

  let audio_ayats = $derived([...Array(nb_ayats).keys()].map(
    (i) =>
      "https://cdn.islamic.network/quran/audio/128/ar.alafasy/" +
      (ayat_before + i + 1) +
      ".mp3",
  ));

  function startTimer() {
    setTimeout(() => {
      // start with basmala
      current_surah_audio = $surah;
      audio.src = audio_ayats[0];
      audio.play();
    }, 0);
  }

  function next_ayah(nb_ayats, ayah) {
    if (ayah + 1 < nb_ayats) {
      audio.src = audio_ayats[ayah + 1];
      audio.play();
    }
  }

  let paused = -1; // -1 not yet started
  function pause_resume() {
    if (paused === -1) {
      startTimer();
      paused = 0;
    } else if (paused) {
      if ($ayah == 0) {
        audio.src = audio_ayats[0];
        audio.play();
      } else {
        audio.play();
      }
      paused = 0;
    } else {
      audio.pause();
      paused = 1;
    }
  }
</script>

<main class="bg-surface-700 text-white">
  <NavBar />
  <Surah {verses} {tafsir_update} {tafsir_nb} {tafsir_txt} />
  <BottomBar {pause_resume} {current_surah_ar_name} />

  <audio
    onended={() => {
      if (current_surah_audio != $surah) {
        paused = -1;
        current_surah_audio = $surah;
      } else {
        next_ayah(nb_ayats, $ayah++);
      }
    }}
    bind:this={audio}
  ></audio>
</main>
