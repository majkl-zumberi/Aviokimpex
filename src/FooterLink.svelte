<script>
  import { _ } from "svelte-i18n";
  import { link } from "svelte-spa-router";

  export let path, label;
</script>

<li>
  <div role="link" tabindex="-1">
    <a use:link class="ul-hover-effect text-gray-700" href={path}>
      {$_(`links.${label}`, {
        default: "",
      })}
    </a>
  </div>
</li>
