<script>
  import { createEventDispatcher } from "svelte";
  import It from "./components/icons/It.svelte";
  import Eu from "./components/icons/Eu.svelte";

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
  role="menuitem"><It/></button>
<button
  on:click={() => switchLocale("en")}
  class="z-50 block bg-gray-100 px-4 py-2 text-sm text-gray-700 hover:bg-gray-300"
  role="menuitem"><Eu/></button>

<style>
  button {
    z-index: 999 !important;
    width: 25px;
    height: 25px;
  }
</style>


