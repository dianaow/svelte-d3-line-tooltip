<script>
  import { onMount } from "svelte"
	import { csv } from "d3-fetch"
  import LineChart from "./LineChart.svelte"

  let data = []
 	onMount(
		async () => {
		  data = await csv('../src/data/aapl.csv')
        .then((raw) => {
          raw.forEach(d => {
            d['close'] = +d['close']
          })
          return raw;
        });
    }
	)
</script>

<div class="wrapper">
  {#if data.length > 0}
    <LineChart {data} />
  {/if}
</div>

<style>
  .wrapper {
    padding: 15px;
  }
</style>
