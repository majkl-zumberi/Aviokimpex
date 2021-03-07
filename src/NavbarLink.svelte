<script>
  import { createEventDispatcher } from "svelte";
  import { _ } from "svelte-i18n";
  import { link, location } from "svelte-spa-router";

  export let path, label, isMobile;
  let desktopViewClass =
    "text-gray-300 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium";
  let mobileViewClass =
    "text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium";
  const dispatch = createEventDispatcher();
  function closeNavbar() {
    console.log("sas");
    dispatch("close");
  }
</script>

<a
  use:link
  href={path}
  class={isMobile ? mobileViewClass : desktopViewClass}
  class:bg-gray-900={path == $location}
  on:click={closeNavbar}
>
  {$_(`links.${label}`, {
    default: "",
  })}
</a>
