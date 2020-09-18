<script context="module">
  import requests from "../data/requests.js";

  export async function preload() {
    try {
      const usStats = await requests.usStats();
      const historicUS = await requests.historicUS();
      const statesData = await requests.statesData();
      return { usStats, historicUS, statesData, };
    } catch (e) {
      console.log(e);
    }
  }
</script>

<script>
  import CovidStat from "../components/CovidStat.svelte";
  import CovidChart from "../components/CovidChart.svelte";
  import TableContainer from "../components/TableContainer.svelte";

  export let usStats;
  export let historicUS;
  export let statesData;
  console.log(statesData, "statesData");
  // console.log(historicUS, "historicUS");
  // console.log(usStats, "usStats");
</script>

<svelte:head>
  <title>Covid 19 US Tracker</title>
</svelte:head>

<div class="section header">
  <div class="container">
    <h1>Covid 19 - US</h1>
  </div>
</div>

<CovidStat {...usStats} />
<CovidChart historicData={historicUS} title="COVID-19 US"/>
<TableContainer data={statesData}/>
