<script>
  import TableFilter from "./TableFilter.svelte";
  import Table from "./Table.svelte";

  export let data;
  $: states = data;

  let stateNameFilter = ""
  $: states = data.filter(d => d.fullStateName.toLowerCase().startsWith(stateNameFilter.toLowerCase()));

  let sortBy = "name";
  $: {
    switch (sortBy) {
      case 'deaths':
        states = states.sort((a,b) => removeComma(b.deaths) - removeComma(a.deaths));
        break;
      case 'tested':
        states = states.sort((a,b) => removeComma(b.tested) - removeComma(a.tested));
        break;
      case 'cases':
        states = states.sort((a,b) => removeComma(b.cases) - removeComma(a.cases));
        break;
      default:
        states = states.sort((a,b) => a.state > b.state);
    }
  }

  const removeComma = (string) => parseInt(string.replaceAll(',', ''));
</script>

<TableFilter bind:stateName={stateNameFilter} bind:sortBy={sortBy} />
<Table {states} {stateNameFilter} />
