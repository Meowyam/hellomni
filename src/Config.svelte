<script>
  import Icon from 'svelte-awesome'
  import { faGithub } from '@fortawesome/free-brands-svg-icons'
  
  let name = 'Name'
  let website = {name:'My Personal Website', url:'my.website'}
  let workwebsite = {name: 'My Work Website', url: 'mywork.website'}
  let git = 'My Github Username'

  import { onMount } from 'svelte'
  let gitData = [];

  const getGitrepos = async function() {
    const response = await fetch("https://api.github.com/users/"+git+"/repos")
    const json = await response.json()
    gitData = json
  }
</script>

<style>
  input.openInput {
    background: white;
    border-right: 0;
      color:black;
      margin-right: -2px;
    }
    input.closeInput {
      border-left: 0;
      margin-left: 0;
    }
    section {
      display: flex;
      flex-direction: column;
      margin-bottom: 1rem;
      border-bottom: 1px solid #aaa;
      padding-bottom: 1rem;
    }
  </style>

  <section>

    <div>
      <input bind:value={name}>
    </div>

    <div>
      <input bind:value={website.name}>
      <input class=openInput readonly disabled value="http://" size=5><input bind:value={website.url} class=closeInput>
    </div>

    <div>
      <input bind:value={workwebsite.name}>
      <input class=openInput readonly disabled value="http://" size=5><input bind:value={workwebsite.url} class=closeInput>
    </div>

    <div>
      <input bind:value={git} on:change={getGitrepos}>
    </div>

  </section>

  <section>

    Hello. My name is {name}!

  </section>

  <section>

    <a href=http://{website.url}>{website.name}</a>

    <a href=http://{workwebsite.url}>{workwebsite.name}</a>

  </section>

<section>

  <span class="item">
    <Icon data={faGithub}></Icon>
      <a href=http://github.com/{git}>{git}</a>
  </span>

  {#each gitData as link}
    <li>
      {link}
    </li>
  {/each}

</section>
