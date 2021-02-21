<script>
  import ArticleByDescription from "./ArticleByDescription.svelte";
  import ArticleCategory from "./ArticleCategory.svelte";
  import ArticleSubcategory from "./ArticleSubcategory.svelte";

  export let params = {};
  let subcategory;
  let filterByArticleName;
  function getParameterByName(name, url = window.location.href) {
    name = name.replace(/[\[\]]/g, "\\$&");
    var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
      results = regex.exec(url);
    if (!results) return null;
    if (!results[2]) return "";
    return decodeURIComponent(results[2].replace(/\+/g, " "));
  }

  $: {
    filterByArticleName = getParameterByName("articleName");
    subcategory = getParameterByName("subcategory");
  }
</script>

<!-- <p>The current page is: {$location}</p>
<p>The querystring is: {$querystring}</p>
<p>id categoria {params.id_category}</p> -->
{#if filterByArticleName}
  <!-- user requested to display article by description name -->
  <ArticleByDescription articleName={filterByArticleName} />
{:else if subcategory == true}
  <!-- user requested to display all articles related to subcategory-->
  <ArticleSubcategory
    id_category={params.id_category}
    id_parent_category={params.id_parent_category}
  />
{:else}
  <!-- user requested to display all articles by main category -->
  <ArticleCategory id_parent_category={params.id_parent_category} />
{/if}
