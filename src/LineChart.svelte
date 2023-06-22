<script>
  import { max } from "d3-array";
  import { scaleLinear, scaleTime } from "d3-scale";
  import Line from "./lib/Line.svelte";
  import AxisX from "./lib/AxisX.svelte";
  import AxisY from "./lib/AxisY.svelte";
  import HoverEvents from "./lib/HoverEvents.svelte";
  import Tooltip from "./lib/Tooltip.svelte";
  
  export let data

  const margin = { top: 30, right: 50, bottom: 30, left: 40 };

  let height = 600;
  let width = 400;

  let innerHeight = height - margin.top - margin.bottom;
  $: innerWidth = width - margin.left - margin.right;

  const yScale = scaleLinear()
    .domain([0, max(data, d => d.close)]) // INPUT
    .range([innerHeight, 0]); // OUTPUT

  const minDate = new Date(data[0].date);
  const maxDate = new Date(data[data.length - 1].date);

  $: xScale = scaleTime()
    .domain([minDate, maxDate]) // INPUT
    .range([0, innerWidth]); // OUTPUT

  const LINE_COLOR = "steelblue";

  let hoveredDate = maxDate
</script>

<div class="chart-container" bind:clientWidth={width}>
  <svg
    {width}
    {height}
    aria-labelledby="chart-title"
    aria-describedby="chart-description"
    role="img"
  >
    <g transform="translate({margin.left} {margin.top})">
      <AxisX
        height={innerHeight}
        {xScale}
        {hoveredDate}
        isUnhovered={hoveredDate === maxDate}
      />
      <AxisY width={innerWidth} {yScale} />
      <Line
        {xScale}
        {yScale}
        data={data}
        color={LINE_COLOR}
        {hoveredDate}
      />  
      {#if hoveredDate}
        <HoverEvents
          width={innerWidth}
          height={innerHeight}
          {xScale}
          {margin}
          {maxDate}
          bind:hoveredDate
        />
      {/if}
      <Tooltip
        {hoveredDate}
        {xScale}
        {yScale}
        data={data}
        color={LINE_COLOR}
      />
    </g>
  </svg>
</div>

