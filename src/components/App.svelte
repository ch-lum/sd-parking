<script>
  console.log('reset')
  import Map from './Map.svelte';
  import Cover from './Cover.svelte';
  import Timeline from './Timeline.svelte';

  let showCover = true;

  function toggleCover() {
    showCover = !showCover;
  }
</script>

<main class="container">
  <Map />
  <div class="wrapper">
    {#if showCover}
        <Cover>
          <button on:click={toggleCover}>Explore Parking Meters</button>
          <h2><br>Or scroll<br><br>↓</h2>
        </Cover>
    {/if}
    
    <button class="reset {!showCover ? 'visible' : ''}" on:click={toggleCover}>Reset</button>
  </div>

  <div class="first_text">
    <p>San diego is well known for being a car-centric city. Blah blah blah blah. Here will go some introduction and discussion about cars</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
    <Timeline />
  </div>
</main>


<style>
  .container {
    display: flex;
    flex-direction: column;
    /* align-items: center;; */
  }

  h1 {
    font-family: Georgia;
    font-size: 4em;
    text-align: center;
  }

  p {
    font-family: Helvetica;
    font-size: 1.5em;
  }

  button, h2 {
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

  h2 {
    text-decoration: none;
    font-style: normal;
    margin: 0px;
    font-weight: normal;
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

  .first_text {
    position: absolute;
    top: 100%;
    width: 100% - 400px;
    border: 2px solid blue;
    text-align: center;
    padding-left: 200px;
    padding-right: 200px;
  }
</style>