<script>
  import TableFilter from "./TableFilter.svelte";
  import Table from "./Table.svelte";

  export let data;
  $: states = data;
</script>

<h1>Table Container</h1>

<TableFilter />
<Table {states} />
