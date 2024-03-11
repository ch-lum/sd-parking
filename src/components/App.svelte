<script>
  console.log('reset')
  import { onMount } from 'svelte';
  import Map from './Map.svelte';
  import Cover from './Cover.svelte';
  import Timeline from './Timeline.svelte';
  import Machine from './Machine.svelte';
  import Narrative from './Narrative.svelte';
  import * as d3 from 'd3';

  let page = 0;
  let lastPage = 6;
  let data = [];

  let showCover = true;

  function toggleCover() {
    showCover = !showCover;
  }

  onMount(async () => {
    const res = await fetch('rad_by_min.csv');
    const csv = await res.text();
    data = d3.csvParse(csv, d3.autoType);
  });
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
    <p>To understand when and where street parking gets used, we took a typical day in 2023, Thursday, March 16, and plotted the number of active parking meters over the course of the day.</p>
    <Timeline />
  </div>

  {#if page !== lastPage}
    <div class= "narrative">
      <Narrative bind:page bind:lastPage bind:data />
    </div>
  {/if}

  <div class="machine">
    <Machine bind:data />
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

  .narrative {
    position: absolute;
    top: 100%;
    transform: translateY(3450px);
    width: 100%;
    background-color: rgba(255, 255, 255, 0);
    z-index: 2;
    border: 2px dashed green;
  }
</style>