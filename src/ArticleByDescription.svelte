<script>
  import { Collection } from "sveltefire";
  import ArticleListContainer from "./ArticleListContainer.svelte";

  export let articleName = "";
</script>

<div class="p-4">
  <section class="text-gray-600 body-font">
    <div class="container px-5 py-24 mx-auto">
      <div class="flex flex-wrap -m-4">
        <Collection
          path={"articoli"}
          query={(ref) =>
            ref
              .orderBy("descrizione")
              .startAt(articleName.toLowerCase())
              .endAt(articleName.toLowerCase() + "~")
              .startAt(articleName.toUpperCase())
              .endAt(articleName.toUpperCase() + "~")}
          traceId={"readArticles"}
          log
          let:data={articles}
        >
          {#each articles as article}
            {#if articles.length < 3}
              <ArticleListContainer
                categoryName=""
                class="lg:w-full sm:w-full md:w-full"
                {article}
              />
            {:else}
              <ArticleListContainer categoryName="" {article} />
            {/if}
          {/each}

          <div slot="loading">Loading...</div>

          <div slot="fallback">Unable to display comments...</div>
        </Collection>
      </div>
    </div>
  </section>
</div>
