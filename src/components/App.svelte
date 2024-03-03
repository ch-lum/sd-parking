<script>
  console.log('reset')
  import Map from './Map.svelte';
  import Cover from './Cover.svelte';

  let showCover = true;

  function toggleCover() {
    showCover = !showCover;
  }
</script>

<main>
  <Map />
  {#if showCover}
      <Cover>
        <button on:click={toggleCover}>Explore</button>
        <p><br>Or scroll<br><br>↓</p>
      </Cover>
  {/if}
  
  <button class="reset {!showCover ? 'visible' : ''}" on:click={toggleCover}>Reset</button>
</main>


<style>
  button, p {
    font-family: Helvetica;
    font-size: 2.5em;
    color: rgba(95, 95, 95, 1);
    background-color: rgba(58, 58, 58, 0);
    border: 2px solid rgba(51, 51, 51, 0);
    border-radius: 5px;
    text-decoration: underline dotted;
    font-style: italic;
    z-index: 3;
  }

  p {
    text-decoration: none;
    font-style: normal;
    margin: 0px;
  }

  button:hover {
    color: rgba(58, 58, 58, 0.5);
  }

  button.reset {
    position: absolute;
    bottom: 50px;
    left: 50px;
    opacity: 0;
    transition: opacity 0.5s ease-in-out;
    z-index: 0;
  }

  button.reset.visible {
    opacity: 1;
    z-index: 3;
  }
</style>