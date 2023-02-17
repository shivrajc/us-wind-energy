<script>
  import { createEventDispatcher } from 'svelte';
  import turbine from '../assets/turbine.svg';

  const dispatch = createEventDispatcher();

  export let screen;
  export let fill;
  export let x;
  export let y;
  export let r;
  export let stroke;
  export let text;
  export let rotate;

	function forwardHover(event) {
		dispatch('hover', {text, x:event.x, y:event.y});
	}

	function forwardLeave(event) {
		dispatch('leave', {text, x:event.x, y:event.y});
	}
</script>

<defs>
  <pattern id="image" x="0%" y="0%" height="100%" width="100%"
            viewBox="0 0 256 256">
    <image x="0%" y="0%" width="256" height="256" xlink:href="{turbine}"></image>
  </pattern>
</defs>

<!-- svelte-ignore a11y-mouse-events-have-key-events -->
<circle 
  cx={x} 
  cy={y} 
  r="{r}" 
  fill="{rotate ? 'url(#image)' : fill}" 
  class:rotate={rotate}
  class="{text}"
  stroke={stroke}
  on:mouseover={forwardHover}
  on:mouseleave={forwardLeave}
  style="pointer-events:{rotate ? 'unset' : 'none'}"
  >
</circle>

<text 
  class="state-label" 
  x={x} 
  y={y} 
  fill="" 
  text-anchor="middle" 
  dominant-baseline="middle" 
  dy="1" 
  style="font-size={screen === 'desktop' ? 12 : 11}px; pointer-events:none">
    {text}
</text>



<style>
  @keyframes rotate{
    from{ transform: rotate(-360deg); }
    to{ transform: rotate(360deg); }
  }

  .rotate {
    transform-box: fill-box;
    transform-origin: center;
    animation-name: rotate;
    animation-duration: 12s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
  }

  .state-label {
    font-size: 12px;
    font-weight: bold;
  }    
</style>