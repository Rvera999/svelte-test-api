<script>
  import Character from './lib/character.svelte'
  let characters=[];
  let page=1;
  async function loadCharacters(){
    const response= await fetch('https://rickandmortyapi.com/api/character?page='+page);
    const data=await response.json();
    characters=data.results;
  }
  function nextPage(){
    page++;
    loadCharacters()
  }
  function previousPage(){
    page--;
    loadCharacters()
  }
  loadCharacters()
</script>
<h1 class="title" >Rick And Morty Svelte</h1>

<div class="container" >
  <div class="btns" >
    <button class="btn1" disabled={page==1} on:click={previousPage} >Previous</button>
    <button class="btn2" disabled={page==42} on:click={nextPage}>Next</button>
  </div>
  
  <div class="grid" >
    {#each characters as character}
    <Character {character}/>
    {/each}
  </div>
</div>