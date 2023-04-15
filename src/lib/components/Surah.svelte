<script>
    import Basmala from "./Basmala.svelte";
    import {ayah} from "../store"
    export let verses, tafsir_update;
</script>

<div dir="rtl" class="snap snap-y snap-mandatory scroll-view">
    <Basmala />
    <br class="snap-start table-zebra" />

    {#each verses as ayah_txt, i (ayah_txt.na)}
        <button
            class="snap-start ayah_button table-cell"
            on:click={() => {
                tafsir_update(i);
            }}
            ><label for="tafsir-modal" class:current={$ayah === i} class="justif "
                >{ayah_txt["text"]}</label
            >۝</button
        >
        <!--  <span class=" rtl ayah_counter table-cell w-20">
            {"\u{FD3F}" + (i + 1) + "\u{FD3E}"} 
            ۝
        </span>
       ۝  -->
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

