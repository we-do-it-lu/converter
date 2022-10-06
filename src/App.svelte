<script>
import Character from './lib/Character.svelte'

  let characters = [];
  let page = 7;

  async function loadCharcters() {
    const response = await fetch("https://rickandmortyapi.com/api/character?page=" + page);
    const data = await response.json();
    characters = data.results;
  }

  loadCharcters();

  function nextPage(){
    page++;
    loadCharcters();
  }

  function previousPage(){
    page--;
    loadCharcters();
  }

</script>

<h1>Hello World</h1>




<div class="container">
  <div class="btns">
    <button on:click={previousPage} disabled={page===1}>Previous</button>
    <button on:click={nextPage}>Next</button>
  
  </div>
  <div class="grid">
{#each characters as character}
<Character character={character}/>
{/each}
</div>
</div>