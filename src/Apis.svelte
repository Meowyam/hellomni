<script>

  import { Config } from './Config.svelte'

  import { onMount } from 'svelte'
  let gitData = [];

  onMount(async function() {
    const response = await fetch("https://api.github.com/users/"+git+"/repos")
    const json = await response.json()
    gitData = json
  })

</script>
{@debug Config}

{#each gitData as text}
  <li>
    {hellotext}
  </li>
{/each}

