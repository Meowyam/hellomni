<script>
  import Icon from 'svelte-awesome'
  import { faGithub } from '@fortawesome/free-brands-svg-icons'

  import { git } from './stores.js'

  let twitter = 'My Twitter Username'

  let repos = []

  const getGitrepos = async function() {
    const response = await fetch("https://api.github.com/users/"+git+"/repos")
    const json = await response.json()
    const gitData = json.map(value => ({'name': value.name, 'url': value.html_url, 'date': new Date(value.updated_at)}) )
    repos = gitData.sort((a,b) => b.date - a.date).slice(0,3)
  }

  const getTweets = async function() {
  }

  let name = 'Name'
  let website = {name:'My Personal Website', url:'my.website'}
  let workwebsite = {name: 'My Work Website', url: 'mywork.website'}
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
  .lastupdated {
    font-style: italic;
    color: #ccc;
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
    <input bind:value={$git} on:change={getGitrepos}>
  </div>

  <div>
    <input bind:value={twitter} on:change={getTweets}>
  </div>

</section>

<section>

  Hello. My name is {name}!

</section>

<section>

  <a href=http://{website.url} title="personal website">{website.name}</a>

  <a href=http://{workwebsite.url} title="work website">{workwebsite.name}</a>

</section>

<section>

  <span class="item">
    <Icon data={faGithub}></Icon>
      <a href=http://github.com/{git}>{git}</a>
  </span>

  Last 3 updated repos

  {#each repos as repo}
    <li>
      <a href={repo.url} title="{repo.name} git repository">{repo.name}</a>
      <span class="lastupdated">last updated {repo.date.toString().substr(0,16)}</span>
    </li>
  {/each}

</section>
