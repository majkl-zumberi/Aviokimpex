<script>
  import { Collection, Doc } from "sveltefire";
  import ArticleBreadcrumb from "./ArticleBreadcrumb.svelte";
  import ArticleListContainer from "./ArticleListContainer.svelte";

  export let id_parent_category;
</script>

<Doc
  path={`categoria/${id_parent_category}`}
  log
  let:data={mainCategory}
  let:ref={categoryRef}
  on:data={(e) => console.log(e.detail.data)}
  on:ref
>
  <ArticleBreadcrumb
    categoryLabel={mainCategory.nome}
    categoryPath="/articles/category/nosubcategory/{id_parent_category}?subcategory=false"
  />
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
                let:data={articles}
                let:ref={articlesRef}
                let:last={firstComment}
                let:first={lastComment}
                on:data
                on:ref
              >
                {#each articles as article}
                  <ArticleListContainer
                    categoryName={category.nome}
                    {article}
                  />
                {/each}

                <div slot="loading">Loading...</div>

                <div slot="fallback">Unable to display articles...</div>
              </Collection>
            {/each}

            <div slot="loading">Loading...</div>

            <div slot="fallback">Unable to display articles...</div>
          </Collection>
        </div>
      </div>
    </section>
  </div>
  <span slot="loading">Loading...</span>
  <span slot="fallback">Error...</span>
</Doc>
