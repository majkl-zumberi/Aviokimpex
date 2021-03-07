<script>
  import { locale } from "svelte-i18n";
  import LangIcon from "./LangIcon.svelte";
  import LocaleSwitcher from "./LocaleSwitcher.svelte";
  import NavbarLink from "./NavbarLink.svelte";
  import { setupI18n } from "./services/i18n";

  let menuOpen = false;
  let dropDownOpen = false;
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
  function toggleMenu() {
    menuOpen = !menuOpen;
  }
  function toggleDropDown() {
    dropDownOpen = !dropDownOpen;
    !menuOpen && dropDownOpen && toggleMenu();
  }
</script>

<nav class="bg-gray-800">
  <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8">
    <div class="relative flex items-center justify-between h-16">
      <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
        <!-- Mobile menu button-->
        <button
          on:click={toggleMenu}
          class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white"
          aria-expanded="false"
        >
          <span class="sr-only">Open main menu</span>
          <!-- Icon when menu is closed. -->
          <!--
              Heroicon name: outline/menu
  
              Menu open: "hidden", Menu closed: "block"
            -->
          <svg
            class="block h-6 w-6"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            aria-hidden="true"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16M4 18h16"
            />
          </svg>
          <!-- Icon when menu is open. -->
          <!--
              Heroicon name: outline/x
  
              Menu open: "block", Menu closed: "hidden"
            -->
          <svg
            class="hidden h-6 w-6"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            aria-hidden="true"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            />
          </svg>
        </button>
      </div>
      <div
        class="flex-1 flex items-center justify-center sm:items-stretch sm:justify-start"
      >
        <div class="flex-shrink-0 flex items-center">
          <img
            class="hidden lg:block h-11 w-auto"
            src="/images/Logo-Kimpex.png"
            alt="Workflow"
          />
        </div>
        <div class="hidden sm:block sm:ml-6">
          <div class="flex space-x-4">
            <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
            {#each routes as { path, label }}
              <NavbarLink {path} {label} isMobile={false} />
            {/each}
          </div>
        </div>
      </div>
      <div
        class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0"
      >
        <!-- Profile dropdown -->
        <div class="ml-3 relative">
          <div>
            <button
              on:click={toggleDropDown}
              class="flex"
              id="user-menu"
              aria-haspopup="true"
            >
              <span class="sr-only">Open user menu</span>
              <LangIcon />
            </button>
          </div>
          <!--
              Profile dropdown panel, show/hide based on dropdown state.
  
              Entering: "transition ease-out duration-100"
                From: "transform opacity-0 scale-95"
                To: "transform opacity-100 scale-100"
              Leaving: "transition ease-in duration-75"
                From: "transform opacity-100 scale-100"
                To: "transform opacity-0 scale-95"
            -->
          <div
            class="z-50 origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white ring-1 ring-black ring-opacity-5"
            class:opacity-0={!dropDownOpen}
            role="menu"
            aria-orientation="vertical"
            aria-labelledby="user-menu"
          >
            <LocaleSwitcher
              value={$locale}
              on:closeProfile={toggleDropDown}
              on:locale-changed={(e) => setupI18n({ withLocale: e.detail })}
            />
          </div>
        </div>
      </div>
    </div>
  </div>

  <!--
      Mobile menu, toggle classes based on menu state.
  
      Menu open: "block", Menu closed: "hidden"
    -->
  <div class="hidden sm:hidden" class:hidden={!menuOpen} class:block={menuOpen}>
    <div class="px-2 pt-2 pb-3 space-y-1">
      <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
      {#each routes as { path, label }}
        <NavbarLink {path} {label} isMobile={true} on:close={toggleMenu} />
      {/each}
    </div>
  </div>
</nav>
