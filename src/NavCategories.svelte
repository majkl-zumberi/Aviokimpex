<script>
  import { link } from "svelte-spa-router";
  import { Collection } from "sveltefire";
</script>

<nav
  class="absolute mx-auto px-6 py-6 bg-white bg-opacity-70 w-full  top-0 z-50"
>
  <Collection
    path={"categoria"}
    log
    let:data={categories}
    let:ref={categoryRef}
    on:data={(e) => console.log(e.detail.data)}
    on:ref={(e) => console.log({ e })}
  >
    {#each categories as category}
      <div class="dropdown">
        <a
          class="text-sm text-gray-700 uppercase font-bold leading-5 mx-4 md:my-0"
          use:link
          href="/articles/category/nosubcategory/{category.id}?subcategory=false"
          >{category.nome}</a
        >
        <div class="dropdown-content">
          <Collection
            path={category.ref.collection("sottocategoria")}
            log
            let:data={subcategories}
            let:ref={subCategoriesRef}
            on:data={(e) => console.log(e.detail.data)}
          >
            {#each subcategories as subcategory}
              <a
                use:link
                href="/articles/category/{subcategory.id}/{category.id}?subcategory=true"
                >{subcategory.nome}</a
              >
            {/each}

            <div slot="loading">
              <button type="button" class="bg-rose-600 ..." disabled>
                <svg
                  class="animate-spin -ml-1 mr-3 h-5 w-5 text-white"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                >
                  <circle
                    class="opacity-25"
                    cx="12"
                    cy="12"
                    r="10"
                    stroke="currentColor"
                    stroke-width="4"
                  />
                  <path
                    class="opacity-75"
                    fill="currentColor"
                    d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
                  />
                </svg>
                loading...
              </button>
            </div>

            <div slot="fallback">Unable to display subcategories...</div>
          </Collection>
        </div>
      </div>
    {/each}

    <div slot="loading">
      <button type="button" class="bg-rose-600 ..." disabled>
        <svg
          class="animate-spin -ml-1 mr-3 h-5 w-5 text-white"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
        >
          <circle
            class="opacity-25"
            cx="12"
            cy="12"
            r="10"
            stroke="currentColor"
            stroke-width="4"
          />
          <path
            class="opacity-75"
            fill="currentColor"
            d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
          />
        </svg>
        loading...
      </button>
    </div>

    <div slot="fallback">Unable to display categories...</div>
  </Collection>
</nav>

<style>
  .dropdown {
    position: relative;
    display: inline-block;
  }

  .dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  }

  .dropdown-content a {
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
  }

  .dropdown-content a:hover {
    background-color: #f1f1f1;
  }

  .dropdown:hover .dropdown-content {
    display: block;
  }
</style>
