<script>
  console.log('reset')
  import Map from './Map.svelte';
  import Cover from './Cover.svelte';
  import Timeline from './Timeline.svelte';
  import Machine from './Machine.svelte';
  import Radial from './Radial.svelte';

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
          <h2><br>And scroll<br>↓</h2>
        </Cover>
    {/if}
    
    <button class="reset {!showCover ? 'visible' : ''}" on:click={toggleCover}>Reset</button>
  </div>

  <div class="first_text">
    <p>San Diego County has a population of 3.2 Million people, and if you've ever tried to go anywhere in rush hour before, you know that quite a sizeable proprotion of 
    those people drive Though bonus fact, not as bad as it could since San Diego County is the 5th most populated, but only 18th on Traffic Severity, so it's not as bad as
    it could be. I'm not sure that'll make the wait on the commute any easier though.
    
     But once you finally get downtown after a few hours of traffic, you have to do the one thing everyone dreads: Finding Parking. Or more accurately, finding street Parking
     instead of shelling out large amounts of money to private parking lots. 
     </p>
     <p>
     We'll be covering some interesting tidbits and insights, but feel more than free to explore on your 
     own as well!
    </p>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
    <Timeline />
  </div>

  <div class="machine">
    <Machine />
    <!-- <Radial /> -->
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
    font-size: 1.2em;
    padding: 20px;
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
    width: 100%;
    border: 2px solid blue;
    text-align: left;
    /* padding-left: 200px;
    padding-right: 200px; */
  }

  .machine {
    display: flex;
    flex-wrap: wrap;
    position: absolute;
    top: 100%;
    transform: translateY(3450px);
    width: 100%;
    border: 2px solid red;
    text-align: left;
    /* padding-left: 200px;
    padding-right: 200px; */
  }
</style>