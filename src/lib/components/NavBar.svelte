<script>
  // @ts-nocheck
  import { quran } from "../values/quran_summerizing";
  import { ayah, surah } from "../store";
  let surats = quran.map((i) => i["name_translations"]["ar"]);

</script>

<div class="clearfix sticky top-0 navbar bg-base-100 z-50">
  <div class="navbar-start">
    <div class="dropdown">
      <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
      <!-- svelte-ignore a11y-label-has-associated-control -->
      <label tabindex="0" class="btn btn-ghost btn-circle">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          ><path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 6h16M4 12h16M4 18h7"
          /></svg
        >
      </label>
      <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
      <ul
        tabindex="0"
        class="menu menu-compact dropdown-content mt-3 p-2 shadow bg-base-100 rounded-box w-52 scrollable fixed block overflow-y-scroll h-80"
      >
        {#each surats as s, i}
          <li>
            <button
              on:click={() => {
                surah.update((n) => i);
                ayah.set(0)
              }}>{s}</button
            >
          </li>
        {/each}
      </ul>
    </div>
  </div>
  <div class="navbar-center">
    <!-- svelte-ignore a11y-missing-attribute -->
    <a class="btn btn-ghost normal-case text-xl">Quran</a>
  </div>
  <div class="navbar-end">
    <button class="info btn btn-ghost btn-circle">ℹ︎</button>
  </div>
</div>

<style>
  .info {
    border: 2px solid;
    height: 25px;
    min-height: 25px;
    width: 25px;
  }
  .clearfix:before,
  .clearfix:after {
    content: ".";
    display: block;
    height: 0;
    overflow: hidden;
  }
  .clearfix:after {
    clear: both;
  }
  .clearfix {
    zoom: 1;
  } /* IE < 8 */
</style>

