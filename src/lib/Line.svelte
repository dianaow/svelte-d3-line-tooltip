<script>
    export let data;
    export let xScale;
    export let yScale;
    export let color;
    export let hoveredDate;

    $: dataBeforeHover = data.filter((d) => new Date(d.date) <= hoveredDate);
    $: dataAfterHover = data.filter((d) => new Date(d.date) > hoveredDate);

    import { line } from "d3-shape";
    $: lineGenerator = line()
        .x((d) => xScale(new Date(d.date)))
        .y((d) => yScale(d.close));
</script>

<path
    d={lineGenerator(dataBeforeHover)}
    stroke={color}
    fill="transparent"
    stroke-width="2"
/>

<path
    d={lineGenerator(dataAfterHover)}
    stroke={color}
    fill="transparent"
    stroke-width="2"
    opacity=".35"
/>
