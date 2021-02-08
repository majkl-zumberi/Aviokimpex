<script>
  import { createEventDispatcher } from "svelte";

  export let value = "it";
  const dispatch = createEventDispatcher();
  function switchLocale(lang) {
    dispatch("locale-changed", lang);
    dispatch("closeProfile");
  }
</script>

<a
  on:click={() => switchLocale("it")}
  class="z-50 block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
  role="menuitem">Italiano</a
>
<a
  on:click={() => switchLocale("en")}
  class="z-50 block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
  role="menuitem">English</a
>

<style>
  a {
    z-index: 999 !important;
  }
</style>
