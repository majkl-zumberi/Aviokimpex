<script>
  import { _ } from "svelte-i18n";
  import { link } from "svelte-spa-router";
  import { Collection } from "sveltefire";
</script>

<div
  class="wrapper bg-gray-100 border-b-2 -mt-8 bg-white overflow-hidden mx-auto max-w-md rounded shadow-lg"
>
  <h3 class="bg-grey-lightest px-8 mt-10 py-6 font-semibold">
    {$_("ListCategories.allCategories", {
      default: "Tutte le categorie",
    })}
  </h3>

  <div class="question-wrap mx-8 mt-2">
    <Collection
      path={"categoria"}
      log
      let:data={categories}
      let:ref={categoryRef}
      on:data={(e) => console.log(e.detail.data)}
      on:ref={(e) => console.log({ e })}
    >
      {#each categories as category}
        <details class="question py-4 border-b border-grey-lighter">
          <summary class="flex items-center font-bold"
            >{category.nome}
            <button class="ml-auto border-none">
              <svg
                class="fill-current opacity-75 w-4 h-4 -mr-1"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                ><path
                  d="M12.95 10.707l.707-.707L8 4.343 6.586 5.757 10.828 10l-4.242 4.243L8 15.657l4.95-4.95z"
                /></svg
              >
            </button>
          </summary>

          <div class="mt-4 leading-normal text-md flex flex-col">
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
                  class="hover:bg-gray-300 py-2 px-1 text-left"
                  >{subcategory.nome}
                </a>
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
        </details>
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
  </div>
</div>

<style>
  details {
    user-select: none;
  }

  details summary svg {
    transform: rotate(90deg);
  }

  details[open] summary svg {
    transform: rotate(-90deg);
  }

  details[open] summary ~ * {
    animation: ease-opacity-t-b 0.5s ease;
  }

  summary {
    cursor: pointer;
  }

  svg {
    transition: all 0.3s;
  }

  /* TO JE TO - TO JE TAJ */
  summary::-webkit-details-marker {
    display: none;
  }

  :focus {
    outline: none;
  }

  .show-more {
    display: flex;
    padding-top: 40px;
  }

  .show-more a {
    display: inline-block;
    margin: 20px auto;
    padding: 12px 12px;
    color: #69a4fc;
    text-decoration: none;
    border: 1px solid rgba(105, 164, 252, 0.8);
    border-radius: 100px;
  }

  .modal {
    font-family: -apple-system, BlinkMacSystemFont, avenir next, avenir,
      helvetica neue, helvetica, ubuntu, roboto, noto, segoe ui, arial,
      sans-serif;
  }

  .modal__overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal__container {
    background-color: #fff;
    padding: 30px;
    max-width: 500px;
    max-height: 100vh;
    border-radius: 4px;
    overflow-y: auto;
    box-sizing: border-box;
  }

  .modal__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .modal__title {
    margin-top: 0;
    margin-bottom: 0;
    font-weight: 600;
    font-size: 1.25rem;
    line-height: 1.25;
    color: #00449e;
    box-sizing: border-box;
  }

  .modal__close {
    background: transparent;
    border: 0;
  }

  .modal__header .modal__close:before {
    content: "\2717";
  }

  .modal__content {
    margin-top: 2rem;
    margin-bottom: 2rem;
    line-height: 1.5;
    color: rgba(0, 0, 0, 0.8);
  }

  .modal__btn {
    font-size: 0.875rem;
    padding-left: 1rem;
    padding-right: 1rem;
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
    background-color: #e6e6e6;
    color: rgba(0, 0, 0, 0.8);
    border-radius: 0.25rem;
    border-style: none;
    border-width: 0;
    cursor: pointer;
    -webkit-appearance: button;
    text-transform: none;
    overflow: visible;
    line-height: 1.15;
    margin: 0;
    will-change: transform;
    -moz-osx-font-smoothing: grayscale;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-transform: translateZ(0);
    transform: translateZ(0);
    transition: -webkit-transform 0.25s ease-out;
    transition: transform 0.25s ease-out;
    transition: transform 0.25s ease-out, -webkit-transform 0.25s ease-out;
  }

  .modal__btn:focus,
  .modal__btn:hover {
    -webkit-transform: scale(1.05);
    transform: scale(1.05);
  }

  .modal__btn-primary {
    background-color: #00449e;
    color: #fff;
  }

  /**************************  Demo Animation Style
\**************************/
  @keyframes mm-fadeIn {
    from {
      opacity: 0;
    }

    to {
      opacity: 1;
    }
  }

  @keyframes mm-slideIn {
    from {
      transform: translateY(35%);
    }

    to {
      transform: translateY(0);
    }
  }

  .micromodal-slide[aria-hidden="false"] .modal__overlay {
    animation: mm-fadeIn 0.3s cubic-bezier(0, 0, 0.2, 1);
  }

  .micromodal-slide[aria-hidden="false"] .modal__container {
    animation: mm-slideIn 0.3s cubic-bezier(0, 0, 0.2, 1);
  }

  .micromodal-slide .modal__container,
  .micromodal-slide .modal__overlay {
    will-change: transform;
  }

  .modal[aria-hidden="true"] {
    display: none;
  }
</style>
