<script>
    import Header from './Header.svelte';
    import Footer from './Footer.svelte';
    import Map from './Map.svelte';
    import Legend from './Legend.svelte';
    import Tooltip from './Tooltip.svelte';
    import { data } from '../data/data';

    export let screen;

    let width = screen === 'desktop' ? 1100 : 460;
    let height = screen === 'desktop' ? 760 : 420;
    $: colWidth = width / 11;      // Calculate cell size for each state of 11 columns
    $: rowHeight = height / 8;     // Calculate cell size for each state of 8 rows
  
    const colorLegend = ["<100 mw", "100-1K mw", "1K-5K mw", "5K-7K mw", "7K-10K mw", "10K+ mw"];
    const colorDomain = [0, 100, 1000, 5000, 10000, 15000];
    const colorRange = ['#f0f9e8','#ccebc5','#a8ddb5','#7bccc4','#43a2ca','#0868ac'];
    const strokeColorRange = ['#ccebc5','#a8ddb5','#7bccc4','#43a2ca','#0868ac', '#064b7b'];
  
    let hoveredData;
    let dim = {x:null, y:null};

    function handleMouseOver(event) {
          hoveredData = event.detail.text;
          dim.x = event.detail.x;
          dim.y = event.detail.y;
          document.querySelector(`.${event.detail.text}`).setAttribute("style", "stroke: black; stroke-width:4");
        }
        
        function handleMouseLeave(event) {
          hoveredData = null;
          document.querySelector(`.${event.detail.text}`).setAttribute("style", "stroke: unset; stroke-width:unset");
    }


  </script>

<main>
  <div class="header">
    <Header {screen} />    
  </div>

  <div class="viz-container"  >      
    <svg id="svg" {width} {height}>
      <Map 
        {screen} 
        {colWidth} 
        {rowHeight} 
        {colorDomain} 
        {colorRange} 
        {strokeColorRange} 
        on:hover={handleMouseOver}
        on:leave={handleMouseLeave}
        />    
    </svg>
  </div>
  
  <div class="legend">
    <Legend {screen} {colorLegend} {colorRange} />
  </div>    
  
  <div class="footer">
    <Footer {screen} />
  </div>

  {#if hoveredData}
    <Tooltip data={$data.filter(d => d.code === hoveredData)[0]} {dim}/>
  {/if}

</main>

<style>
  main {
    height: 100vh;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  
  }

  .viz-container {
    width: 100%;
    height: 100%;
    /* background: hotpink; */
    flex-grow: 1;
    position: relative;
  }

  .header {
    height: 160px;
    width: 100%;
    padding: 20px;
    border-bottom: 1px solid rgb(200, 200, 200);  
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .footer {
    height: 60px;
    width: 100%;
  }

  svg {
    /* border: 1px solid gray; */
    margin: auto;
    position: absolute;
    top: 0; left: 0; bottom: 0; right: 0;
  }

  .legend {
      height: 100px;
      width: 100%;
      text-align: center;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
  }

</style>