<script>
  import { _ } from "svelte-i18n";
</script>

<!-- ABOUT US AND IMAGE -->

<section class="text-gray-600 body-font">
  <div
    class=" container mx-auto flex px-5 py-24 md:flex-row flex-col items-center "
  >
    <div class="lg:max-w-lg lg:w-full md:w-1/2 w-5/6 mb-10 md:mb-0">
      <img
        class="object-cover object-center rounded"
        alt="hero"
        src="/images/Profile.jpg"
      />
    </div>
    <div
      class="lg:flex-grow md:w-1/2 lg:pl-24 md:pl-16 flex flex-col md:items-start md:text-left items-center text-center"
    >
      <h1
        class="title-font sm:text-4xl text-3xl mb-4 font-medium text-gray-900"
      >
        {$_("about.who", {
          default: "Chi siamo?",
        })}
        <br class="hidden lg:inline-block" />
      </h1>
      <p class="mb-8 leading-relaxed">
        {$_("about.marinoni", {
          default:
            "Pietro Marinoni professionista da quasi quarantanni nel settore aeronautico, civile e militare per la commercializzazione parti di ricambio, nel 2000 fonda la Kimpex, un’azienda in grado di servire a 360° ricambistica e assistenza minuteria, attrezzature,prodotti chimici e lubrificanti.",
        })}
      </p>
      <div class="flex justify-center" />
    </div>
  </div>
</section>

<!-- BOTTOM FEATURE -->

<section class="text-gray-600 body-font">
  <div class="container px-5 py-24 mx-auto">
    <div
      class="flex items-center lg:w-3/5 mx-auto border-b pb-10 mb-10 border-gray-200 sm:flex-row flex-col"
    >
      <div
        class="sm:w-32 sm:h-32 h-20 w-20 sm:mr-10 inline-flex items-center justify-center rounded-full bg-indigo-100 text-indigo-500 flex-shrink-0"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="black"
          width="48px"
          height="48px"
        >
          <path d="M0 0h24v24H0z" fill="none" />
          <path
            d="M21 16v-2l-8-5V3.5c0-.83-.67-1.5-1.5-1.5S10 2.67 10 3.5V9l-8 5v2l8-2.5V19l-2 1.5V22l3.5-1 3.5 1v-1.5L13 19v-5.5l8 2.5z"
          />
        </svg>
      </div>
      <div class="flex-grow sm:text-left text-center mt-6 sm:mt-0">
        <h2 class="text-gray-900 text-lg title-font font-medium mb-2">
          know How
        </h2>
        <p class="leading-relaxed text-base">
          example text, example text, example text, example text, example text,
          example text, example text.
        </p>
      </div>
    </div>

    <div
      class="flex items-center lg:w-3/5 mx-auto border-b pb-10 mb-10 border-gray-200 sm:flex-row flex-col"
    >
      <div class="flex-grow sm:text-left text-center mt-6 sm:mt-0">
        <h2 class="text-gray-900 text-lg title-font font-medium mb-2">
          Rapidità
        </h2>
        <p class="leading-relaxed text-base">
          example text, example text, example text, example text, example text,
          example text, example text.
        </p>
      </div>

      <div
        class="sm:w-32 sm:order-none order-first sm:h-32 h-20 w-20 sm:ml-10 inline-flex items-center justify-center rounded-full bg-indigo-100 text-indigo-500 flex-shrink-0"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="black"
          width="48px"
          height="48px"
        >
          <path d="M0 0h24v24H0z" fill="none" />
          <path
            d="M20.38 8.57l-1.23 1.85a8 8 0 0 1-.22 7.58H5.07A8 8 0 0 1 15.58 6.85l1.85-1.23A10 10 0 0 0 3.35 19a2 2 0 0 0 1.72 1h13.85a2 2 0 0 0 1.74-1 10 10 0 0 0-.27-10.44zm-9.79 6.84a2 2 0 0 0 2.83 0l5.66-8.49-8.49 5.66a2 2 0 0 0 0 2.83z"
          />
        </svg>
      </div>
    </div>

    <div class="flex items-center lg:w-3/5 mx-auto sm:flex-row flex-col">
      <div
        class="sm:w-32 sm:h-32 h-20 w-20 sm:mr-10 inline-flex items-center justify-center rounded-full bg-indigo-100 text-indigo-500 flex-shrink-0"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="black"
          width="48px"
          height="48px"
        >
          <path d="M0 0h24v24H0V0z" fill="none" />
          <path
            d="M20 2H4c-1 0-2 .9-2 2v3.01c0 .72.43 1.34 1 1.69V20c0 1.1 1.1 2 2 2h14c.9 0 2-.9 2-2V8.7c.57-.35 1-.97 1-1.69V4c0-1.1-1-2-2-2zm-5 12H9v-2h6v2zm5-7H4V4l16-.02V7z"
          />
        </svg>
      </div>

      <div class="flex-grow sm:text-left text-center mt-6 sm:mt-0">
        <h2 class="text-gray-900 text-lg title-font font-medium mb-2">
          Vasto Assortimento
        </h2>
        <p class="leading-relaxed text-base">
          example text, example text, example text, example text, example text,
          example text, example text.
        </p>
      </div>
    </div>
  </div>
</section>
