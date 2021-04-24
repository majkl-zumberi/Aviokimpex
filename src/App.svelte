<script>
  import firebase from "firebase/app";
  import "firebase/auth";
  import "firebase/firestore";
  import "firebase/performance";
  import { locale } from "svelte-i18n";
  import Router from "svelte-spa-router";
  import { FirebaseApp } from "sveltefire";
  import About from "./About.svelte";
  import ArticleDetail from "./components/article/ArticleDetail.svelte";
  import ArticlesList from "./components/article/ArticlesList.svelte";
  import Brands from "./Brands.svelte";
  import Contacts from "./Contacts.svelte";
  import Footer from "./components/footer/Footer.svelte";
  import Home from "./Home.svelte";
  import InfoBanner from "./InfoBanner.svelte";
  import Navbar from "./components/navbar/Navbar.svelte";
  import { setupI18n } from "./services/i18n/i18n";

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
  <InfoBanner />
  <FirebaseApp {firebase}>
    <Router
      routes={{
        "/": Home,
        "/about": About,
        "/brands": Brands,
        "/contacts": Contacts,
        "/articles/category/:id_category/:id_parent_category?": ArticlesList,
        "/article/:id": ArticleDetail,
      }}
    />
  </FirebaseApp>
  <Footer />
</div>
