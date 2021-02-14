<script>
  import firebase from "firebase/app";
  import "firebase/auth";
  import "firebase/firestore";
  import "firebase/performance";
  import { locale } from "svelte-i18n";
  import Router from "svelte-spa-router";
  import { FirebaseApp } from "sveltefire";
  import About from "./About.svelte";
  import ArticlesList from "./ArticlesList.svelte";
  import Brands from "./Brands.svelte";
  import Contacts from "./Contacts.svelte";
  import Footer from "./Footer.svelte";
  import Home from "./Home.svelte";
  import Navbar from "./Navbar.svelte";
  import { setupI18n } from "./services/i18n";

  locale.set("it");
  setupI18n({ withLocale: "it" });

  const firebaseConfig = {
    apiKey: _vars.env.apiKey,
    authDomain: _vars.env.authDomain,
    projectId: _vars.env.projectId,
    storageBucket: _vars.env.storageBucket,
    messagingSenderId: _vars.env.messagingSenderId,
    appId: _vars.env.appId,
  };

  firebase.initializeApp(firebaseConfig);
</script>

<div class=" overflow-hidden">
  <Navbar />
  <FirebaseApp {firebase}>
    <Router
      routes={{
        "/": Home,
        "/about": About,
        "/brands": Brands,
        "/contacts": Contacts,
        "/articles/category/:id_category/:id_parent_category?": ArticlesList,
      }}
    />
  </FirebaseApp>
  <Footer />
</div>
