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
    <p>
      San Diego County has a population of 3.2 Million people, and if you've ever tried to go anywhere in rush hour before, you know that quite a sizeable proprotion of 
      those people drive. Though bonus fact, not as bad as it could since San Diego County is the 5th most populated, but only 18th on Traffic Severity, so it's not as bad as
      it could be. I'm not sure that'll make the wait on the commute any easier though.
      
      But once you finally get downtown after a long while of traffic, you have to do the one thing everyone dreads: Finding Parking. Or more accurately, finding street Parking
      instead of shelling out large amounts of money to private parking lots. 
      <br><br>
      So, let's take a look at the parking meters in San Diego, and see if we can't find some patterns in the data. The San Diego Association of Governments (SANDAG) has wonderfully made publicly available ample amounts of data surrounding census, transportation, crime, and more for the San Diego region on their <a href="https://opendata.sandag.org/">open data portal</a>.
    </p>

    <h3>The Meters</h3>
    <p>
      San Diego has 20 different neighborhoods with parking meters with nearly 5 million parking transactions in 2023 coming from 6,000 parking meters. 

      To understand when and where street parking gets used, we took a typical day in 2023, Thursday, March 16, and plotted the number of active parking meters over the course of the day for each neighborhood. Further, the areas are ordered left-to-right the fewest maximum active meters to the most.
    </p>
    <div class="timeline">
      <div class="timeline-comments">
        <p class="annotation" style="top: 7%;">
          The first people to begin parking start to pay at 6:00 AM when the meters first open. The Marina has attractions such as the USS Mideway and Seaport Village, so being at the heart of San Diego might explain their early start.
        </p>

        <p class="annotation" style="top: 15%; left: 10%;">
          By 8:00 AM, the East Village, home of PetCo Park, has the most active meters, which comes as little surprise considering that they have the most parking meters in the city.
        </p>

        <p class="annotation" style="top: 22%; left: 40%;">
          10:00 AM marks the first instance where a wave of meters end their transactions. Keep note of what times have quick drops like this one.
        </p>

        <p class="annotation" style="top: 29%; left: 48%;">
          People arrive in Hillcrest before their noon errands and they cause a spike in active meters before many leave as the hour passes. Perhaps parking is easier if make plans for 12:05.
        </p>

        <p class="annotation" style="top: 36%; left: 48%;">
          Some of the neighborhoods with the fewest meters, such as Point Loma, are far from downtown and only have a few meters. Though, Midtown, with a peak of 1 active meter, has 17 meters in total. Point Loma has the feweset with 8 meters.
        </p>

        <p class="annotation" style="top: 44%; left: 48%;">
          Around 4:00 PM is a sort of parking meter happy hour, with a small lull in the number of total active meters. This is most prominent in Little Italy, which is known for their rich food scene explaining their resurgance around 5.
        </p>
        
        <p class="annotation" style="top: 51%; left: 43%;">
          At 6:00 PM, parking becomes free in most places. This is similar to how parking is free on holidays and Sundays, so we see a huge drop to zero transactions. The Marina in interesting, where only half of its transactions end.
        </p>

        <p class="annotation" style="top: 59%; left: 20%;">
          The last of the meters end their transactions at 8:00 PM. Of the 20 locations, only Gaslamp seemed to manage to avoid the 6 PM drop and truly ends all their meters at 8.
        </p>

        <p class="annotation" style="top: 70%;">
          The night is quiet. Street lights flicker overhead. Parking meters sleep a healthy ten hours each night before they wake back up and get back to it.
        </p>

        <p class="annotation" style="top: 82%;">
          Despite the lack of parking meters, people are still welcome to park on the street. The lack of parking meters from 8 PM to 6 AM indicates a lack of paying instead of a lack of parking. Maybe the best time to park is at night?
        </p>

        <p class="annotation" style="top: 92%; left: -5%; width: 80%; font-size: 1em;">
          This chart ends at 5:00 AM on Friday, March 17th, 2023 and Friday will look like much of the same. 19,171 people used public parking on Thursday and was the seventh most parked-on day of the year. The most parked-on day will come three weeks later, on another Thursday, April 6th.
        </p>
      </div>
      <Timeline />
    </div>
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

  <div class="bibliography">
    <h3>References</h3>
    <p>
      <a href="https://opendata.sandag.org/">SANDAG Open Data Portal</a>
      <a href="https://docs.sandiego.gov/municode/MuniCodeChapter08/Ch08Art06Division01.pdf">San Diego Municipal Code</a>
    </p>

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
    font-size: 1em;
    padding-left: 60px;
    padding-right: 60px;
    text-align: justify;
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

  h3 {
    font-family: Helvetica;
    font-size: 1.4em;
    font-weight: bold;
    padding-left: 60px;
    padding-right: 60px;
    margin-top: 50px;
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
    /* border: 2px solid blue; */
    text-align: left;
    margin-top: 100px;
    /* padding-left: 200px;
    padding-right: 200px; */
  }

  .machine {
    display: flex;
    flex-wrap: wrap;
    position: absolute;
    top: 100%;
    transform: translateY(3500px);
    width: 100%;
    /* border: 2px solid red; */
    text-align: left;
    /* padding-left: 200px;
    padding-right: 200px; */
  }

  .narrative {
    position: absolute;
    top: 100%;
    transform: translateY(3500px);
    width: 100%;
    background-color: rgba(255, 255, 255, 0);
    z-index: 2;
    /* border: 2px dashed green; */
  }

  .timeline {
    z-index: 1;
    background-color: rgba(255, 255, 255, 0);
  }

  .timeline-comments {
    position: absolute;
    left: 50%;
    width: 50%;
    height: 90%;
    text-align: left;
    z-index: 0;
    padding: 0px;
  }

  .annotation {
    position: absolute;
    width: 50%;
    padding: 0px;
    font-size: 0.8em;
    pointer-events: none;
  }
</style>