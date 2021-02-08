<script>
  import { locale } from "svelte-i18n";
  import Router from "svelte-spa-router";
  import About from "./About.svelte";
  import Brands from "./Brands.svelte";
  import Contacts from "./Contacts.svelte";
  import Footer from "./Footer.svelte";
  import Home from "./Home.svelte";
  import Navbar from "./Navbar.svelte";
  import { setupI18n } from "./services/i18n";

  locale.set("it");
  setupI18n({ withLocale: "it" });
</script>

<div class=" overflow-hidden">
  <Navbar />
  <Router
    routes={{
      "/": Home,
      "/about": About,
      "/brands": Brands,
      "/contacts": Contacts,
    }}
  />
  <Footer />
</div>
