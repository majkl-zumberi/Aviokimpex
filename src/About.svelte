<script>
  import { _ } from "svelte-i18n";
  import AboutFeature from './components/About-feature.svelte'
</script>

<!-- ABOUT US AND IMAGE -->

<section class="text-gray-600 body-font">
  <div
    class=" container mx-auto flex px-5 py-24 md:flex-row flex-col items-center rounded-t-full mb-8 md:rounded-full"
  >
    <div class="lg:max-w-lg lg:w-full md:w-1/2 w-5/6 mb-10 md:mb-0">
      <img
        class="object-cover object-center rounded-full"
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
<AboutFeature/>
<style>
  .container{
    background-color: #dbe0e4 !important;
  }
</style>