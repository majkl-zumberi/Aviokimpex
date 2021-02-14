<script>
  import { link, location, querystring } from "svelte-spa-router";
  import { Collection, Doc } from "sveltefire";

  export let params = {};
</script>

<p>The current page is: {$location}</p>
<p>The querystring is: {$querystring}</p>
<p>id categoria {params.id_category}</p>

{#if $querystring == "subcategory=true"}
  <Doc
    path={`categoria/${params.id_parent_category}/sottocategoria/${params.id_category}`}
    log
    let:data={myData}
    let:ref={myRef}
    on:data={(e) => console.log(e.detail.data)}
    on:ref
  >
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
            href="/articles/category/nosubcategory/{params.id_parent_category}?subcategory=false"
            >cerca per categoria generale</a
          >
        </li>
        <li
          class="px-4 text-gray-700 text-sm text-gray-700 uppercase font-bold leading-5 mx-4 md:my-0"
          aria-current="page"
        >
          {myData.nome}
        </li>
      </ol>
    </nav>
    <div class="p-4">
      <section class="text-gray-600 body-font">
        <div class="container px-5 py-24 mx-auto">
          <div class="flex flex-wrap -m-4">
            <Collection
              path={"articoli"}
              query={(ref) =>
                ref.where("idSottocategoria", "==", `${params.id_category}`)}
              log
              let:data={comments}
              let:ref={commentsRef}
              let:last={firstComment}
              let:first={lastComment}
              on:data
              on:ref
            >
              {#each comments as comment}
                <div class="p-4 lg:w-1/3">
                  <div
                    class="h-full bg-gray-100 bg-opacity-75 px-8 pt-16 pb-24 rounded-lg overflow-hidden text-center relative"
                  >
                    <h2
                      class="tracking-widest text-xs title-font font-medium text-gray-400 mb-3"
                    >
                      {myData.nome} |
                      <span
                        class="inline-block py-1 px-2 rounded bg-indigo-50 text-indigo-500 text-xs font-medium tracking-widest"
                        >{comment.marca}</span
                      >
                    </h2>
                    <h1
                      class="title-font sm:text-2xl text-lg uppercase font-medium text-gray-900 mb-1"
                    >
                      {comment.descrizione}
                    </h1>

                    <div
                      class="text-center mt-2 leading-none flex justify-center absolute bottom-0 left-0 w-full py-4"
                    >
                      <span
                        class="text-gray-400 mr-3 inline-flex items-center leading-none text-sm pr-3 py-1 border-r-2 border-gray-200"
                      >
                        <span
                          class="inline-block py-1 px-2 rounded bg-indigo-50 text-indigo-500 text-xs font-medium tracking-widest"
                          >cod. {comment.alternatoPN}-{comment.partNumber}</span
                        >
                      </span>
                      <span
                        class="text-gray-400 inline-flex items-center leading-none text-sm"
                      >
                        <a class="text-indigo-500 inline-flex items-center"
                          >Richiedi quotazione
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
                    </div>
                  </div>
                </div>
              {/each}

              <div slot="loading">Loading...</div>

              <div slot="fallback">Unable to display comments...</div>
            </Collection>
          </div>
        </div>
      </section>
    </div>
    <span slot="loading">Loading...</span>
    <span slot="fallback">Error...</span>
  </Doc>
{:else}
  <p>solo categoria</p>
  <Doc
    path={`categoria/${params.id_parent_category}`}
    log
    let:data={myData}
    let:ref={categoryRef}
    on:data={(e) => console.log(e.detail.data)}
    on:ref
  >
    {myData.nome}
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
            href="/articles/category/nosubcategory/{params.id_parent_category}?subcategory=false"
            >{myData.nome}</a
          >
        </li>
      </ol>
    </nav>
    <div class="p-4">
      <section class="text-gray-600 body-font">
        <div class="container px-5 py-24 mx-auto">
          <div class="flex flex-wrap -m-4">
            <Collection
              path={categoryRef.collection("sottocategoria")}
              log
              let:data={subcategories}
              let:ref={subCategoriesRef}
              on:data={(e) => console.log(e.detail.data)}
            >
              {#each subcategories as category}
                <Collection
                  path={"articoli"}
                  query={(ref) =>
                    ref.where("idSottocategoria", "==", `${category.id}`)}
                  log
                  let:data={comments}
                  let:ref={commentsRef}
                  let:last={firstComment}
                  let:first={lastComment}
                  on:data
                  on:ref
                >
                  {#each comments as comment}
                    <div class="p-4 lg:w-1/3">
                      <div
                        class="h-full bg-gray-100 bg-opacity-75 px-8 pt-16 pb-24 rounded-lg overflow-hidden text-center relative"
                      >
                        <h2
                          class="tracking-widest text-xs title-font font-medium text-gray-400 mb-3"
                        >
                          {category.nome} |
                          <span
                            class="inline-block py-1 px-2 rounded bg-indigo-50 text-indigo-500 text-xs font-medium tracking-widest"
                            >{comment.marca}</span
                          >
                        </h2>
                        <h1
                          class="title-font sm:text-2xl text-lg uppercase font-medium text-gray-900 mb-1"
                        >
                          {comment.descrizione}
                        </h1>

                        <div
                          class="text-center mt-2 leading-none flex justify-center absolute bottom-0 left-0 w-full py-4"
                        >
                          <span
                            class="text-gray-400 mr-3 inline-flex items-center leading-none text-sm pr-3 py-1 border-r-2 border-gray-200"
                          >
                            <span
                              class="inline-block py-1 px-2 rounded bg-indigo-50 text-indigo-500 text-xs font-medium tracking-widest"
                              >cod. {comment.alternatoPN}-{comment.partNumber}</span
                            >
                          </span>
                          <span
                            class="text-gray-400 inline-flex items-center leading-none text-sm"
                          >
                            <a class="text-indigo-500 inline-flex items-center"
                              >Richiedi quotazione
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
                        </div>
                      </div>
                    </div>
                  {/each}

                  <div slot="loading">Loading...</div>

                  <div slot="fallback">Unable to display comments...</div>
                </Collection>
              {/each}

              <div slot="loading">Loading...</div>

              <div slot="fallback">Unable to display comments...</div>
            </Collection>
          </div>
        </div>
      </section>
    </div>
    <span slot="loading">Loading...</span>
    <span slot="fallback">Error...</span>
  </Doc>
{/if}
