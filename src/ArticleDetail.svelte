<script>
  import { Doc } from "sveltefire";
  import ArticleListContainer from "./ArticleListContainer.svelte";
  import ListCategories from "./ListCategories.svelte";

  export let params = {};
</script>

<section class="text-gray-600 body-font">
  <div class="container px-5 py-24 mx-auto">
    <div class="flex flex-wrap -m-4">
      <div class="p-4 lg:w-1/3 sm:w-full">
        <div
          class="h-full  bg-opacity-75 px-8      pb-24 rounded-lg overflow-hidden text-center relative"
        >
          <ListCategories />
        </div>
      </div>
      <Doc path={`articoli/${params.id}`} let:data={articleItem}>
        <!-- Default Slot -->
        <ArticleListContainer
          article={articleItem}
          isInList={false}
          viewLink={false}
        />

        <!-- Only shown when loading -->
        <div slot="loading" />

        <!-- Shown on error or if nothing loads after maxWait time-->
        <div slot="fallback" />
      </Doc>

      <div class="p-4 lg:w-1/3 sm:w-full">
        <div
          class=" bg-gray-100 rounded-lg p-8 flex flex-col md:ml-auto w-full mt-10 md:mt-0"
        >
          <h2 class="text-gray-900 text-lg font-medium title-font mb-5">
            Richiedi quotazione
          </h2>
          <h3 class="text-gray-500 text-base  title-font mb-5">
            Vuoi ricevere maggiori informazioni o una quotazione personalizzata
            su questo articolo? Chiamaci al numero <span class="font-medium"
              >+390302421830</span
            > oppure compila il form
          </h3>
          <div class="relative mb-4">
            <label for="full-name" class="leading-7 text-sm text-gray-600"
              >Full Name</label
            >
            <input
              type="text"
              id="full-name"
              name="full-name"
              class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
            />
          </div>
          <div class="relative mb-4">
            <label for="email" class="leading-7 text-sm text-gray-600"
              >Email</label
            >
            <input
              type="email"
              id="email"
              name="email"
              class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
            />
          </div>
          <div class="relative mb-4">
            <label for="email" class="leading-7 text-sm text-gray-600"
              >Telefono</label
            >
            <input
              type="email"
              id="email"
              name="email"
              class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
            />
          </div>
          <button
            class="text-white uppercase bg-green-400 border-0 py-2 px-8 focus:outline-none hover:bg-indigo-600 rounded text-lg"
            >Invia</button
          >
        </div>
      </div>
    </div>
  </div>
</section>
