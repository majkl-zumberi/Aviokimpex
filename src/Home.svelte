<script>
  import { Collection } from "sveltefire";
  import Slideshow from "./Slideshow.svelte";
</script>

<h1>HOME PAGE</h1>
<Collection
  path={"categoria"}
  log
  let:data={categories}
  let:ref={categoryRef}
  on:data={(e) => console.log(e.detail.data)}
  on:ref={(e) => console.log({ e })}
>
  {#each categories as category}
    <pre>{category.nome}</pre>
    <pre>{category.id}</pre>
    <Collection
      path={category.ref.collection("sottocategoria")}
      log
      let:data={subcategories}
      let:ref={subCategoriesRef}
      on:data={(e) => console.log(e.detail.data)}
    >
      {#each subcategories as subcategory}
        <pre>{subcategory.nome} appartiene alla categoria {category.nome}</pre>
        <pre>{subcategory.id}</pre>
      {/each}

      <div slot="loading">Loading...</div>

      <div slot="fallback">Unable to display subcategories...</div>
    </Collection>
  {/each}

  <div slot="loading">Loading...</div>

  <div slot="fallback">Unable to display categories...</div>
</Collection>
<Slideshow />
