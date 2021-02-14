<script>
  import { querystring } from "svelte-spa-router";
  import ArticleCategory from "./ArticleCategory.svelte";
  import ArticleSubcategory from "./ArticleSubcategory.svelte";

  export let params = {};
</script>

<!-- <p>The current page is: {$location}</p>
<p>The querystring is: {$querystring}</p>
<p>id categoria {params.id_category}</p> -->

{#if $querystring == "subcategory=true"}
  <ArticleSubcategory
    id_category={params.id_category}
    id_parent_category={params.id_parent_category}
  />
{:else}
  <ArticleCategory id_parent_category={params.id_parent_category} />
{/if}
