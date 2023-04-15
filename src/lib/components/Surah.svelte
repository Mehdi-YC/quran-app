<script>
    import Basmala from "./Basmala.svelte";
    import { surah, ayah } from "../store";
    export let verses, tafsir_update;
    import PageSeparation from "./PageSeparation.svelte";
    import { new_page } from "../values/new_page";

</script>

<div dir="rtl" class="snap snap-y snap-mandatory scroll-view">
    <Basmala />
    <br class="snap-start table-zebra" />

    {#each verses as ayah_txt, i (ayah_txt.na)}
        {#if new_page[`${$surah + 1},${i}`] != undefined}
            <PageSeparation page_number={new_page[`${$surah + 1},${i}`]} />
        {/if}
        <button
            class="snap-start ayah_button table-cell"
            on:click={() => {
                tafsir_update(i);
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
        padding: 60px 15% 0 15%;
        text-align: center;
        height: 75vh;
        overflow-y: scroll;
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
