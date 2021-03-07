<script>
  import { _ } from "svelte-i18n";
  import { link } from "svelte-spa-router";

  export let categoryName,
    article,
    isInList = true,
    viewLink = true;
</script>

<div class="p-4 lg:w-1/3 sm:w-full {$$props.class}">
  <div
    class:h-full={isInList}
    class="bg-gray-100 bg-opacity-75 px-8 pt-16 pb-24 rounded-lg overflow-hidden text-center relative"
  >
    <h2
      class="tracking-widest text-xs title-font font-medium text-gray-400 mb-3"
    >
      {categoryName && categoryName != undefined ? `${categoryName} |` : ""}
      <span
        class="inline-block py-1 px-2 rounded bg-indigo-50 text-indigo-500 text-xs font-medium tracking-widest"
        >{article.marca}</span
      >
    </h2>
    <h1
      class="title-font sm:text-2xl text-lg uppercase font-medium text-gray-900 mb-1"
    >
      {article.descrizione}
    </h1>

    <div
      class="text-center mt-2 leading-none flex justify-center absolute bottom-0 left-0 w-full py-4"
    >
      <span
        class="text-gray-400 mr-3 inline-flex items-center leading-none text-sm pr-3 py-1 border-r-2 border-gray-200"
      >
        <span
          class="inline-block py-1 px-2 rounded bg-indigo-50 text-indigo-500 text-xs font-medium tracking-widest"
          >cod. {article.alternatoPN}-{article.partNumber}</span
        >
      </span>

      {#if viewLink}
        <span
          class="text-gray-400 inline-flex items-center leading-none text-sm"
        >
          <a
            use:link
            href="/article/{article.id}"
            class="text-indigo-500 inline-flex items-center py-1 px-2 hover:bg-indigo-50"
            >{$_("order.request", {
              default: "Richiedi quotazione",
            })}
            <svg
              class="w-4 h-4 ml-2"
              viewBox="0 0 24 24"
              stroke="currentColor"
              stroke-width="2"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M5 12h14" />
              <path d="M12 5l7 7-7 7" />
            </svg>
          </a>
        </span>
      {/if}
    </div>
  </div>
</div>
