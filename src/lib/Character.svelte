<script>
  export let character

</script>

<div class="character">
  <img src={character.image} alt={character.name}/>
  <h1 class="title">{character.name}</h1>
  <h3>Origine: {character.origin.name}</h3>
  
  </div>