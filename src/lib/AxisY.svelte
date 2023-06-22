<script>
    export let width;
    export let yScale;
</script>

{#each yScale.ticks(10) as tick}
    <text
        x="0"
        dx="-6"
        y={yScale(tick)}
        text-anchor="end"
        dominant-baseline="middle"
        fill="#999"
    >
        {tick}
    </text>
    <line x1="0" x2={width} y1={yScale(tick)} y2={yScale(tick)} stroke="#dcdcdc" />
{/each}
<line x1="0" x2={width} y1={yScale(0)} y2={yScale(0)} stroke="#000" />
<text x="-22" y="0">↑ Daily close ($)</text>

<style>
    text {
        font-size: 0.7rem;
        fill: #000
    }
</style>
