<script>  
    import { data } from '../data/data';
    import { format, scaleQuantile } from 'd3';
    import State from './State.svelte';
     
    export let screen;
    export let colWidth;
    export let rowHeight;
    export let colorDomain;
    export let colorRange;
    export let strokeColorRange;    

    const colorScale = scaleQuantile()
                            .domain(colorDomain)
                            .range(colorRange);

    const strokeColorScale = scaleQuantile()
                            .domain(colorDomain)
                            .range(strokeColorRange);

    const data2 = [...$data];

    // update the data with xy coordinates for each state in the grid map
    data.update(d => {
      for(let i=1; i<=8; i++) {
        for(let j=1; j<=11; j++) {
            data2.forEach(function(item, index) {
                if(item.row === i && item.col === j) {
                    item.x = (colWidth * j) - (colWidth / 2);
                    item.y = (rowHeight * i) - (rowHeight / 2);
                }
            })
        }
      }  
      return data2;
    });



</script>



{#each $data as state}
    {#if state.wind_turbines !== ""}
        // State circle with color coding based on installled capacity
        <State 
            {screen} 
            x={state.x} 
            y={state.y} 
            r={screen === 'desktop' ? 40 : 16} 
            fill={colorScale(state.installed_capacity_mw)} 
            stroke="none" 
            rotate={false} 
            text={state.code} 

        />

        // State circle with wind turbine image rotating
        <State 
            {screen} 
            x={state.x} 
            y={state.y} 
            r={screen === 'desktop' ? 40 : 16} 
            fill={colorScale(state.installed_capacity_mw)} 
            stroke="{strokeColorScale(state.installed_capacity_mw)}" 
            rotate={true} 
            text={state.code} 
            on:hover
            on:leave
        />

        // State circle with state code label
        <State 
            {screen} 
            x={state.x} 
            y={state.y} 
            r={screen === 'desktop' ? 14 : 10} 
            fill="white" 
            stroke="gray" 
            rotate={false} 
            text={state.code}

        />
    {:else}
        <State 
            {screen} 
            x={state.x} 
            y={state.y} 
            r={screen === 'desktop' ? 40 : 16} 
            fill="none" 
            stroke="lightgray" 
            rotate={false} 
            text={state.code} 
        />        

        <State 
            {screen} 
            x={state.x} 
            y={state.y} 
            r={screen === 'desktop' ? 14 : 10} 
            fill="none" 
            stroke="none" 
            rotate={false} 
            text={state.code} 
        />
    {/if}
{/each}

