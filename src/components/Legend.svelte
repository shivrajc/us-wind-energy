<script>    
    export let colorLegend;
    export let colorRange;    
    export let screen;
</script>

<div class="wrapper">
    <div class="legend-wrapper">
        {#each colorLegend as legend, index}
            <div class="legend" style="background: {colorRange[index]}; width: {screen === 'desktop' ? 90 : 70}px">
            </div>
        {/each}
    </div>
    <div class="label-wrapper">
        {#each colorLegend as legend, index}
            <div class="legend" style="width: {screen === 'desktop' ? 90 : 70}px">
                <span class="legend-label" style="font-size: {screen === 'desktop' ? 14 : 11}px">
                    {legend}
                </span>
            </div>            
        {/each}
    </div>
</div>
<style>
    .legend-wrapper {
        display: flex;
    }

    .legend {
        height: 12px;
        width: 90px;        
    }

    .label-wrapper {
        display: flex;
    }

    .legend-label {
        font-size: 14px;
        color: gray;
        display: flex;
        justify-content: center;
    }
</style>
