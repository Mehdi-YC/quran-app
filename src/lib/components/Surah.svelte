<script>
    import Basmala from "./Basmala.svelte";
    import { surah, ayah } from "../store";
    import PageSeparation from "./PageSeparation.svelte";
    import { new_page } from "../values/new_page";
    import TafsirModal from "./TafsirModal.svelte";

    let {verses, tafsir_update,tafsir_nb,tafsir_txt} = $props();


    let show_tafsir = $state(false);
</script>

<TafsirModal {tafsir_nb} {tafsir_txt} bind:show_tafsir={show_tafsir} />
<div dir="rtl" style="height:90vh" class="bg-surface-700 text-white text-2xl scroll-view snap-y snap-mandatory overflow-y-scroll">
    <Basmala />
    <br class="snap-start table-zebra" />

    {#each verses as ayah_txt, i (ayah_txt.na)}
        {#if new_page[`${$surah + 1},${i}`] != undefined}
            <PageSeparation page_number={new_page[`${$surah + 1},${i}`]} />
        {/if}
        <button
            class="snap-start ayah_button table-cell"
            onclick={() => {
                tafsir_update(i);
                show_tafsir = true;
            }}
            ><label
                id="verse-{i}"
                for="tafsir-modal"
                class:current={$ayah === i}
                class="justif">{ayah_txt["text"]}</label
            >۝</button
        >
    {/each}
</div>

<style>
    .justif {
        text-align: justify;
    }
    .current {
        color: cadetblue;
    }
    .scroll-view {
        z-index: 10;
        position: fixed;
        padding: 60px 8% 0 8%;
        text-align: center;
        height: 75vh;
        overflow-y: scroll;
    }
    .ayah_button {
    display: block;
    width: 100%;
    padding: 1rem;
    scroll-snap-align: start;
    }
    /* Hide scrollbar for Chrome, Safari and Opera */
    .scroll-view::-webkit-scrollbar {
        display: none;
    }

    /* Hide scrollbar for IE, Edge and Firefox */
    .scroll-view {
        -ms-overflow-style: none; /* IE and Edge */
        scrollbar-width: none; /* Firefox */
    }
</style>
