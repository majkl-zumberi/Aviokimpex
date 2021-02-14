<script>
  import { location } from "svelte-spa-router";
  import { Collection, Doc } from "sveltefire";
  import ArticleBreadcrumb from "./ArticleBreadcrumb.svelte";
  import ArticleListContainer from "./ArticleListContainer.svelte";

  export let id_parent_category, id_category;
</script>

<Doc
  path={`categoria/${id_parent_category}/sottocategoria/${id_category}`}
  log
  let:data={subCategory}
  on:data={(e) => console.log(e.detail.data)}
  on:ref
>
  <!-- get parent category name for breadcrumb display-->
  <Doc path={`categoria/${id_parent_category}`} let:data={parentCategory}>
    <ArticleBreadcrumb
      subcategoryLabel={subCategory.nome}
      subcategoryPath={$location}
      categoryLabel={parentCategory.nome}
      categoryPath="/articles/category/nosubcategory/{id_parent_category}?subcategory=false"
    />
  </Doc>
  <div class="p-4">
    <section class="text-gray-600 body-font">
      <div class="container px-5 py-24 mx-auto">
        <div class="flex flex-wrap -m-4">
          <Collection
            path={"articoli"}
            query={(ref) =>
              ref.where("idSottocategoria", "==", `${id_category}`)}
            log
            let:data={articles}
            let:ref={articlesRef}
            let:last={firstComment}
            let:first={lastComment}
            on:data
            on:ref
          >
            {#each articles as article}
              <ArticleListContainer categoryName={subCategory.nome} {article} />
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
