<script>
    import {
        fade,
        fly,
        slide
    } from 'svelte/transition';

    import Map from '../components/Map.svelte';
    import ActorStatus from '../components/ActorStatus.svelte';
    let src = 'iot-arch-diagram.png'
    let arch_collapsed = false

    function handle_collapse_click(e) {
        arch_collapsed = !arch_collapsed
    }
</script>

<style>
    .header {
        grid-column: 1 / -1;
    }
    
    h1 {
        font-size: 2.8em;
        text-transform: uppercase;
        font-weight: 700;
        margin: 0 0 0.5em 0;
        text-align: center;
        color: rgba(51, 0, 114, 1)
    }
    
    #architecture__collapse__button {
        z-index: 1;
        /* width: 2.5em; */
        /* height: 1em; */
        /* margin: 0;
        padding: 0; */
        font-size: 150%;
        border: 1px solid rgba(83, 86, 90, 1);
        cursor: pointer;
        /* margin: auto; */
        color: rgba(255, 255, 255, 1);
        border-radius: 1rem;
        margin-right: auto;
        margin-bottom: auto;
        position: absolute;
        top: 0;
        left: -1.5em;
    }
    
    #map {
        grid-column: 1;
    }
    
    button,
    button:link,
    button:visited {
        text-transform: uppercase;
        text-decoration: none;
        /* padding: 1.5rem 1.5rem; */
        /* display: inline-block; */
        border-radius: 3rem;
        -webkit-transition: all 0.2s;
        transition: all 0.2s;
        position: relative;
        font-size: 150%;
        /* border: 1px solid rgba(51, 0, 114, 1); */
        cursor: pointer;
        margin-right: auto;
        margin-bottom: auto;
        /* color: rgba(51, 0, 114, 1); */
        background-color: rgba(51, 0, 114, 1);
    }
    
    button:hover,
    button:link:hover,
    button:visited:hover {
        -webkit-transform: translateY(-3px);
        transform: translateY(-3px);
        -webkit-box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.2);
        box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.2)
    }
    
    button:hover::after,
    button:link:hover::after,
    button:visited:hover::after {
        -webkit-transform: scaleX(1.4) scaleY(1.6);
        transform: scaleX(1.4) scaleY(1.6);
        opacity: 0
    }
    
    button:active,
    button:focus,
    button:link:active,
    button:link:focus,
    button:visited:active,
    button:visited:focus {
        outline: none;
        -webkit-transform: translateY(-1px);
        transform: translateY(-1px);
        -webkit-box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.2);
        box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.2)
    }
    
    button::after {
        content: "";
        display: inline-block;
        height: 100%;
        width: 100%;
        border-radius: 10rem;
        position: absolute;
        top: 0;
        left: 0;
        z-index: -1;
        -webkit-transition: all 0.4s;
        transition: all 0.4s
    }
    
    #architecture__diagram {
        grid-column: 1 / -1;
        grid-row: 2;
        z-index: 2;
        /* height: 90vh; */
    }
    
    #architecture__diagram img {
        width: 100%;
        box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
    }
    
    #architecture__diagram button {
        width: 1em;
    }
</style>

<div class="header">
    <h1>Factory Status</h1>
</div>
<span style="position: relative; grid-row: 2; grid-column: 1 /2;">
<button id="architecture__collapse__button" on:click={handle_collapse_click} in:fade="{{duration: 200}}" out:fade="{{duration: 0}}">
            {arch_collapsed ? "+" : "-"}
</button>
</span> {#if !arch_collapsed}

<div id="architecture__diagram" in:fade="{{duration: 200}}" out:fade="{{duration: 0}}">
    <img {src} alt="architecture diagram">
</div>
{:else}
<div id="map" in:fade="{{duration: 200}}" out:fade="{{duration: 0}}">
    <Map />
</div>
<div id="actor_status" in:fade="{{duration: 200}}" out:fade="{{duration: 0}}">
    <ActorStatus />
</div>
{/if}