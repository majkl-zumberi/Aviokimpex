<script>
  import { createEventDispatcher } from "svelte";

  export let value = "it";
  const dispatch = createEventDispatcher();
  function switchLocale(lang) {
    dispatch("locale-changed", lang);
    dispatch("closeProfile");
  }
</script>

<button
  on:click={() => switchLocale("it")}
  class="z-50 block bg-gray-100 px-4 py-2 text-sm text-gray-700 hover:bg-gray-300"
  role="menuitem">Italiano</button>
<button
  on:click={() => switchLocale("en")}
  class="z-50 block bg-gray-100 px-4 py-2 text-sm text-gray-700 hover:bg-gray-300"
  role="menuitem">English</button>

<style>
  button {
    z-index: 999 !important;
  }
</style>
