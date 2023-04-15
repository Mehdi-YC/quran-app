<script>
  import "./app.css";
  import BottomBar from "./lib/components/BottomBar.svelte";
  import NavBar from "./lib/components/NavBar.svelte";
  import Surah from "./lib/components/Surah.svelte";
  import TafsirModel from "./lib/components/TafsirModel.svelte";
  import { quran } from "./lib/values/quran_summerizing";
  import { tafsir } from "./lib/values/tafsir";
  import { surah,ayah } from "./lib/store";


  var tafsir_nb = 0;
  var tafsir_id_rev, tafsir_txt, ayat_before;

  $: verses = quran[$surah]["verses"];

  $: nb_ayats = quran[$surah]["n_of_ayah"];
  $: ayat_before = quran[$surah]["ayah_before"];

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
      audio.src = audio_ayats[0];
      audio.play();
    }, 0);
  }

  function next_ayah(nb_ayats, ayah) {
    if (ayah + 1 < nb_ayats) {
      audio.src = audio_ayats[ayah + 1];
      audio.play();
      scrollIntoView();
    }
  }

  let paused = -1; // -1 not yet started
  function pause_resume() {
    if (paused === -1) {
      startTimer();
      paused = 0;
    } else if (paused) {
      audio.play();
      paused = 0;
    } else {
      audio.pause();
      paused = 1;
    }
  }

  let scroller;
  function scrollIntoView() {
    const el = scroller.querySelector(".current");
    console.log("scrolling to ", el);
    if (!el) return;
    el.scrollIntoView({
      behavior: "smooth",
    });
  }
</script>

<main>
  <NavBar />
  <Surah bind:this={scroller} {verses} {tafsir_update} />
  <BottomBar {pause_resume}/>
  <TafsirModel {tafsir_nb} {tafsir_txt} />
  <audio
    on:ended={() => {
      next_ayah(nb_ayats, $ayah++);
    }}
    bind:this={audio}
  />
</main>
