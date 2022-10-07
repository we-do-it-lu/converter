<script>
  import { onMount } from "svelte";
  import Coin from "./lib/Coin.svelte";

  let coins = [];

  let coinrakingurl = "https://api.coinranking.com/v2";

  async function loadcoinprices() {
    const response = await fetch(
      coinrakingurl + "/search-suggestions?query=bitco",
      {
        method: "GET",
        headers: {
          "accept-language": "en",
          "Content-type": "application/json;charset=UTF-8",
          "x-access-token": "coinranking65312d3925c14dfa96101df961aa59da1f9acaa7c04395c7",
        },
      }
    );

    const string = await response.text();
    const json = string === "" ? {} : JSON.parse(string);

    if (json) {
      coins = json.data.coins;
    } else {
      alert("HTTP-Error: " + response.status);
    }
  }


  loadcoinprices();

  onMount(() => {
		window.onunhandledrejection = (e) => {
		  console.log('we got exception, but the app has crashed', e);
			// here we should gracefully show some fallback error or previous good known state
			// this does not work though:
			// current = C1; 
			
			// todo: This is unexpected error, send error to log server
			// only way to reload page so that users can try again until error is resolved
			// uncomment to reload page:
			// window.location = "/oi-oi-oi";
		}
	})

</script>

<h1>Bitcoin to FIAT converter</h1>

<div class="container">
  <!-- div class="btns">
    <button on:click={previousPage} disabled={page === 1}>Previous</button>
    <button on:click={nextPage}>Next</button>
  </div -->
  <div class="grid">
    {#each coins as coin}
      <Coin {coin} />
    {/each}
  </div>
</div>
