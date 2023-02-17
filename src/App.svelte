<script>
  import MediaQuery from './MediaQuery.svelte';
  import Main from './components/Main.svelte';
</script>

<main>  
    <MediaQuery query="(min-width: 800px)" let:matches>
      {#if matches}
        <Main screen="desktop"/>
      {/if}
    </MediaQuery>
    
    <!-- <MediaQuery query="(min-width: 480px) and (max-width: 1200px)" let:matches>
      {#if matches}
        <MobileApp />
      {/if}
    </MediaQuery> -->
    
    <MediaQuery query="(max-width: 800px)" let:matches>
      {#if matches}
        <Main screen="mobile"/>
      {/if}
    </MediaQuery>    
</main>

<style>
</style>
