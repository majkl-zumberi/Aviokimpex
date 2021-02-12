<script>
  import { location, querystring } from "svelte-spa-router";

  export let params = {};
</script>

<p>The current page is: {$location}</p>
<p>The querystring is: {$querystring}</p>
<p>id categoria {params.id_category}</p>
