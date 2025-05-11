<script>
    import { ayah } from "../store";
    export let pause_resume;
    export let current_surah_ar_name;

    let isPlaying = false;

    function togglePlayPause() {
        isPlaying = !isPlaying;
        pause_resume();
    }
</script>

<div class="fixed bottom-0 left-0 right-0 flex justify-around items-center bg-background text-2xl py-4 shadow-custom z-50">
    <button
        class="text-primary font-bold"
        on:click={togglePlayPause}
    >
        {#if isPlaying}
            ||
        {:else}
            ▶
        {/if}
    </button>

    <div class="text-secondary font-semibold">
        {current_surah_ar_name} - {$ayah + 1}
    </div>
</div>

<style>
    .shadow-custom {
        box-shadow: 0px -32px 183px -16px rgba(255, 255, 255, 0.192);
    }
</style>