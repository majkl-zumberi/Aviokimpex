<script>
  import { link } from "svelte-spa-router";

  export let categoryPath, categoryLabel, subcategoryPath, subcategoryLabel;
</script>

<nav class="p-8 bg-gray-300" aria-label="breadcrumb">
  <ol
    class="flex leading-none text-indigo-600 divide-double divide-x divide-gray-400"
  >
    <li class="pr-4">
      <a
        use:link
        href="/"
        class="text-sm text-gray-700 uppercase font-bold leading-5 mx-4 md:my-0"
        >Home</a
      >
    </li>
    <li class="px-4">
      <a
        use:link
        class="text-sm text-gray-700 uppercase font-bold leading-5 mx-4 md:my-0"
        href={categoryPath}>{categoryLabel}</a
      >
    </li>
    {#if subcategoryLabel && subcategoryPath}
      <li class="px-4">
        <a
          use:link
          class="text-sm text-gray-700 uppercase font-bold leading-5 mx-4 md:my-0"
          href={subcategoryPath}>{subcategoryLabel}</a
        >
      </li>
    {/if}
  </ol>
</nav>
