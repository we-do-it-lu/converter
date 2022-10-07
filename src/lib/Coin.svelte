<script>
    export let coin  
  </script>
  
  <div class="coin">

    <h1 class="title">{coin.name}</h1>
    <h3>uuid: {coin.uuid}</h3>
    <img src={coin.iconUrl} alt={coin.iconUrl}/>
    <h3>Price: {coin.price}</h3>
    
</div>