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
  ];
</script>

<footer class=" flex justify-center">
  <div class="w-full max-w-screen-lg p-4 md:p-8">
    <div class="flex flex-wrap w-full justify-between mb-4">
      <section class="w-full sm:w-4/12 mb-8 sm:mb-0">
        <img
          class="hidden lg:block h-14 w-auto"
          src="/images/Logo-Kimpex.png"
          alt="kimpex logo"
        />
        <p class="text-gray-800">
          {$_("footer.contacts.headQuarter", {
            default:
              "Kimpex di Pietro Marinoni - Sede Operativa: via Raffaele Da Brescia 25 - 25124 Brescia",
          })}
        </p>
      </section>
      <div class="flex w-full sm:w-8/12 sm:justify-end">
        <section>
          <h1 class="text-gray-800 text-xl mb-2">Link</h1>
          <ul>
            {#each routes as route}
              <li>
                <div role="link" tabindex="-1">
                  <FooterLink {...route} />
                </div>
              </li>
            {/each}
          </ul>
        </section>
        <section class="ml-16 md:ml-24">
          <h1 class="text-gray-800 text-xl mb-2">
            {$_("footer.contacts.keepInTouch", {
              default: "Restiamo in contatto!",
            })}
          </h1>
          <div class="-ml-2" />
          <h1 class="text-gray-800 text-xl mt-4">Email</h1>
          <div class="flex flex-col">
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
