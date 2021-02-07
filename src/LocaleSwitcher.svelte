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
  class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
  role="menuitem">Italiano</a
>
<a
  on:click={() => switchLocale("en")}
  class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
  role="menuitem">English</a
>
