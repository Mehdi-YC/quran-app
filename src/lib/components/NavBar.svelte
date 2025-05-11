<script>
  import { quran } from "../values/quran_summerizing";
  import { ayah, surah } from "../store";
  import InformationModal from "./InformationModal.svelte";

  let surats = quran.map((i) => i["name_translations"]["ar"]);

  let show = $state(false);
  function showToggle() {
    show = !show;
  }
</script>

<div class="bg-surface-800 sticky top-0 z-50  shadow-md">
  <div class="flex items-center justify-between px-4 py-2">
    <!-- Dropdown -->
    <div class="relative">
      <!-- svelte-ignore a11y_consider_explicit_label -->
      <button class="btn btn-ghost btn-circle" onclick={showToggle}>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 6h16M4 12h16M4 18h7"
          />
        </svg>
      </button>

      <!-- Dropdown Menu -->
      {#if show}
        <ul
          class="bg-surface-800 absolute mt-4 p-2  shadow-lg rounded-lg w-52 max-h-80 overflow-y-scroll z-50"
        >
          {#each surats as s, i}
            <li>
              <button
                class="block py-2 px-4 w-full text-left "
                onclick={() => {
                  surah.update((n) => i);
                  ayah.set(0);
                  showToggle();
                }}
              >
                {s}
              </button>
            </li>
          {/each}
        </ul>
      {/if}
    </div>

    <!-- Center Title -->
    <div class="text-xl font-semibold">Quran</div>

    <!-- Info Button -->
    <InformationModal />
  </div>
</div>