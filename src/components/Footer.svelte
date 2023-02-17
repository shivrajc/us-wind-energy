<script>
    import home from '../assets/home.png';

    export let screen;
</script>

<footer style="font-size: {screen === 'desktop' ? 0.9 : 0.7}rem">
    <a href="http://shivrajc.com" target="blank">
        <img src="{home}" alt="home icon" style="margin-right:{screen === 'desktop' ? 40 : 24}px"/>
    </a> 
    
    <p class:footer-p-desktop={screen==='desktop'} class:footer-p-mobile={screen==='mobile'}>
        source: #makeovermonday | howmuch.net
    </p> 
    
    <p class:footer-p-desktop={screen==='desktop'} class:footer-p-mobile={screen==='mobile'}>
        icons: flaticon.com
    </p>
    
</footer>

<style>
    footer {
        position: fixed;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 50px;
        background: #f4f4f4;
        display: flex;
        justify-content: center;
        align-content: center;
        align-items: center;
        color: rgb(98, 98, 98);
        border-top: 1px solid rgb(200, 200, 200);
    }

    img {
        width: 20px;
        margin-top: 6px;
    }

    .footer-p-desktop {
        margin-right: 40px;
        padding-top: 2px;
    }

    .footer-p-mobile {
        margin-right: 20px;
        padding-top: 2px;
    }    
</style>