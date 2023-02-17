<script>
    export let screen;
</script>

<header>
    <h1 class=main-header style="font-size: {screen === 'desktop' ? 48 : 32}px">
        Wind Energy in the US - 2018
    </h1>
    <p class="sub-header" style="font-size: {screen === 'desktop' ? 24 : 16}px">
        Texas, Oklahoma, and Iowa are the leading producers of wind energy in 2018
    </p> 

</header>

<style>
    h1 {
        font-size: 48px;
        margin-bottom: 12px;
    }

    .sub-header {
        font-size: 24px;
        font-weight: normal;
        color: rgb(84, 84, 84);
    }
</style>