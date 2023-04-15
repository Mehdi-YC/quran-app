<script>
     import { surah,ayah } from "../store";
    export let pause_resume;
</script>

<div class="btm-nav text-2xl">
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label class="swap">

    </label>
    <label class="swap">
        <input
            on:click={() => {
                pause_resume();
            }}
            type="checkbox"
        />
        <div class="swap-off">▶</div>
        <div class="swap-on font-black">||</div>
    </label>
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label class="swap">
        {$surah+1}-{$ayah+1}
    </label>
</div>

<style>

</style>
