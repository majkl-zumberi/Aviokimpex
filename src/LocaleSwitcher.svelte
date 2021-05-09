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
  class="bg-gray-100 hover:bg-grey text-grey-darkest font-bold py-2 px-4 rounded inline-flex items-center"
  role="menuitem">
  <It />
  <span></span>
</button>
<button
  on:click={() => switchLocale("en")}
  class="bg-gray-100 hover:bg-grey text-grey-darkest font-bold py-2 px-4 rounded inline-flex items-center"
  role="menuitem"><Eu/></button>

<style>
  button {
    z-index: 999 !important;
  }
</style>


