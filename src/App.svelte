<script>
  import "./app.css";
  import BottomBar from "./lib/components/BottomBar.svelte";
  import NavBar from "./lib/components/NavBar.svelte";
  import Surah from "./lib/components/Surah.svelte";
  import TafsirModal from "./lib/components/TafsirModal.svelte";
  import { quran } from "./lib/values/quran_summerizing";
  import { tafsir } from "./lib/values/tafsir";
  import { surah, ayah } from "./lib/store";
  var current_surah_audio;
  var tafsir_nb = 0;
  var tafsir_id_rev, tafsir_txt, ayat_before, current_surah_ar_name;

  $: verses = quran[$surah]["verses"];

  $: nb_ayats = quran[$surah]["n_of_ayah"];
  $: ayat_before = quran[$surah]["ayah_before"];
  $: current_surah_ar_name = quran[$surah]["name_translations"]["ar"];
  function tafsir_update(i) {
    tafsir_nb = i;
    tafsir_id_rev = nb_ayats - 1 - tafsir_nb;
    tafsir_txt = tafsir[$surah][tafsir_id_rev]["text"];
  }

  //audio stuff
  let audio, audio_ayats;

  $: audio_ayats = [...Array(nb_ayats).keys()].map(
    (i) =>
      "https://cdn.islamic.network/quran/audio/128/ar.alafasy/" +
      (ayat_before + i + 1) +
      ".mp3"
  );

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
      //scrollIntoView();
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

<main>
  <NavBar />
  <Surah {verses} {tafsir_update} />
  <BottomBar {pause_resume} {current_surah_ar_name} />
  <TafsirModal {tafsir_nb} {tafsir_txt} />
  <audio
    on:ended={() => {
      if (current_surah_audio != $surah) {
        paused = -1;
        current_surah_audio = $surah;
      } else {
        next_ayah(nb_ayats, $ayah++);
      }
    }}
    bind:this={audio}
  />
</main>
