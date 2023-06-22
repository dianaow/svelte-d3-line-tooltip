<script>
    export let height;
    export let xScale;
    export let hoveredDate;
    export let isUnhovered;

    // Format our ticks as short date strings
    import { timeFormat } from "d3-time-format";
    const dateFormat = timeFormat("%b %Y");

    const TICK_LENGTH = 8;

    $: ticks = isUnhovered ? xScale.ticks(12) : [hoveredDate];
</script>

{#each ticks as tick}
    <line
        x1={xScale(tick)}
        x2={xScale(tick)}
        y1={height}
        y2={height + TICK_LENGTH}
        stroke="#000"
    />
    <text
        x={xScale(tick)}
        y={height + TICK_LENGTH}
        dy="6"
        dominant-baseline="hanging"
        text-anchor="middle"
        fill="#999"
    >
        {isUnhovered ? dateFormat(tick) : timeFormat("%e %b %Y")(tick)}
    </text>
{/each}

<style>
    text {
        font-size: 0.7rem;
        fill: #000
    }
</style>
