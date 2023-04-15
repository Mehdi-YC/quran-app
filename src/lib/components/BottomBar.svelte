<script>
    import { ayah } from "../store";
    export let pause_resume;
    export let current_surah_ar_name;
</script>

<div class="btm-nav text-2xl shadow">
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label class="swap" />
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
        {current_surah_ar_name}-{$ayah + 1}
    </label>
</div>

<style>
    .shadow {
        box-shadow: 0px -32px 183px -16px rgba(255, 255, 255, 0.192);
    }
</style>
