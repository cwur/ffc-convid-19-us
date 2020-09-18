<script context="module">
  import stateNames from "../data/stateNames.js";
  import requests from '../data/requests.js';

  export async function preload(page) {
    const state = page.params["state"];
    if (
      stateNames.find((stateName) => stateName.abbreviation === state) ===
      undefined
    ) {
      this.error(404, "State Not Found");
      return;
    }

    try {
      let stats = await requests.stateStats(state);
      let historicStats = await requests.historicState(state);
      return { state, stats, historicStats };
    } catch (e) {
      this.error(
        500,
        "There was an error in calling the api, please try again in 5 minutes."
      );
      return;
    }
  }

</script>

<script>
  import CovidStat from "../components/CovidStat.svelte";
  import CovidChart from "../components/CovidChart.svelte";
  import TableContainer from "../components/TableContainer.svelte";

  export let state;
  export let stats;
  export let historicStats;
</script>

<svelte:head>
  <title>Covid 19 US - {state}</title>
</svelte:head>

<div class="section header">
  <div class="container">
    <h1>Covid 19 - {state}</h1>
  </div>
</div>

<CovidStat {...stats}/>
<CovidChart historicData={historicStats} title="COVID-19 {state}"/>
