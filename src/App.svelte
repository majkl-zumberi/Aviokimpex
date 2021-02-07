<script>
	 import Router, {link} from 'svelte-spa-router';
	 import Home from './Home.svelte';
	 import Navbar from './Navbar.svelte';
	 import About from './About.svelte';
	 import Brands from './Brands.svelte';
	 import Contacts from './Contacts.svelte';
</script>

<Navbar/>
<Router routes={{
	'/':Home,
	'/about':About,
	'/brands':Brands,
	'/contacts':Contacts,
}} />