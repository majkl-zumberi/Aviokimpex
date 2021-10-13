<script>
  import { _ } from "svelte-i18n";
  import FooterLink from "./FooterLink.svelte";

  let routes = [
    {
      path: "/",
      label: "home",
    },
    {
      path: "/about",
      label: "aboutUs",
    },
    {
      path: "/brands",
      label: "brands",
    },
    {
      path: "/contacts",
      label: "contactUs",
    },
    {
      path: "/gallery",
      label: "gallery",
    },
  ];
</script>

<footer class=" flex justify-center">
  <div class="w-full max-w-full p-4 md:p-8">
    <div class="flex flex-wrap flex-wrap md:flex-nowrap w-full justify-between mb-4">

      <section class="w-full sm:w-4/12 mb-8 sm:mb-0">
        <img
          class="block lg:block h-14 w-auto"
          src="/images/Logo-Kimpex.png"
          alt="kimpex logo"
        />
        <br>
        <p>Via Monte Pasubio, 114/b 25014, Castenedolo (BS), Italia</p>
        <p>P.iva 02266020987</p>
        <p>C.F. MRNPTR54S18B157R</p>
        <p>Pec: pec@pec.aviokimpex.com</p>

      </section>
      
      <div class="flex w-full flex-wrap md:flex-nowrap sm:justify-center sm:mb-0">
        <section class="w-1/2">
          <h1 class="text-gray-800 text-xl mb-2 mt-2">Link</h1>
          <ul class="mt-11">
            {#each routes as route}
              <li>
                <div role="link" tabindex="-1">
                  <FooterLink {...route} />
                </div>
              </li>
            {/each}
          </ul>
        </section>

        <section class=" w-1/2 ml-33 md:ml-10 mt-2">
          <h1 class="text-gray-800 text-xl mb-2">
            {$_("footer.contacts.keepInTouch", {
              default: "Restiamo in contatto!",
            })}
          </h1>
          <div class="-ml-2" />
          <h1 class="text-gray-800 text-xl">Email</h1>
          <div class="flex flex-col">
            <a
              class="text-gray-700 ul-hover-effect mt-2"
              href="mailto:amministrazione@aviokimpex.com"
              >amministrazione@aviokimpex.com
            </a>
            <a
              class="text-gray-700 ul-hover-effect"
              href="mailto:pietromarinoni@aviokimpex.com"
              >pietromarinoni@aviokimpex.com
            </a>
            <a
              class="text-gray-700 ul-hover-effect"
              href="mailto:info@aviokimpex.com"
              >info@aviokimpex.com
            </a>
          </div>
        </section>

        <section class="w-full md:ml-24">
          <img
            class="pt-2 block lg:block h-14 w-auto"
            src="/images/AvioKimpexsrl.png"
            alt="aviokimpex logo"
          />
          <br>
          <p>Via Monte Pasubio, 114/b 25014, Castenedolo (BS), Italia</p>
          <p>P.iva 04158520983</p>
          <p>C.F. 04158520983 </p>
          <p>Pec: aviokimpexsrl@pec.it</p>
        </section>

      </div>
    </div>
    <div class="text-center">
      <br /><br />
      <p class="mb-2 text-gray-800">© 2021 | Kimpex di Pietro Marinoni</p>
    </div>
  </div>
</footer>

<style>
  footer {
    background-color: #dbe0e4 !important;
  }
</style>
