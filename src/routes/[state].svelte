<script context="module">
  import stateNames from "../data/stateNames";

  export async function preload(page) {
    console.log(stateNames, page.params["state"]);
    const state = page.params["state"];
    if (
      stateNames.find((stateName) => stateName.abbreviation === state) ===
      undefined
    ) {
      this.error(404, "State Not Found");
      return;
    }

    try {
      return { state };
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
</script>

<svelte:head>
  <title>Covid 19 US - {state}</title>
</svelte:head>

<div class="section header">
  <div class="container">
    <h1>Covid 19 - {state}</h1>
  </div>
</div>

<CovidStat />
<CovidChart />
